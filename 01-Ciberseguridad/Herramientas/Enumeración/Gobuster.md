---
tags:
  - herramientas/enumeracion
---
## ¿Qué es?

Gobuster es una herramienta de seguridad ofensiva de código abierto escrita en Golang, utilizada para la fuerza bruta en servidores web mediante técnicas de [[Enumeración]] rápida. Es ampliamente utilizada por pentesters para el reconocimiento en auditorías de seguridad web.

Corresponde a una herramienta de fuerza bruta para descubrir directorios, archivos y subdominios ocultos en aplicaciones web. Funciona tomando una wordlist (lista de palabras) y probando cada una contra el objetivo, reportando qué existe realmente.

* URI (directorios y archivos) en sitios web.
* Subdominios DNS (con soporte de comodines).
* Nombres de host virtuales en servidores web de destino.
* Depósitos de Amazon S3 y Google Cloud Storage (GCS).
* Abrir servidores TFTP.
* Fuzzing personalizado con parámetros personalizables.

Está diseñado para probadores de penetración, profesionales de seguridad y expertos forenses para realizar evaluaciones de seguridad y reconocimiento.
## Instalación en Fedora

```bash
sudo dnf install gobuster -y
```

En Kali ya viene preinstalado.

## Modos Principales

Gobuster tiene varios modos, los más usados son:

**dir** — busca directorios y archivos ocultos, útil para ver la estructura de directorios de un sitio web y qué archivos contiene. A menudo, las estructuras de directorios de sitios web y aplicaciones web siguen una convención particular, haciéndolas susceptibles a ataques de fuerza bruta usando wordlists:


```bash
gobuster dir -u http://objetivo.com -w /ruta/wordlist.txt
```


**dns** — busca subdominios:

```bash
gobuster dns -d objetivo.com -w /ruta/wordlist.txt
```


**vhost** — busca virtual hosts:

```bash
gobuster vhost -u http://objetivo.com -w /ruta/wordlist.txt
```

## Opciones importantes

|Flag|Qué hace|
|---|---|
|`-u`|URL objetivo|
|`-w`|Ruta a la wordlist|
|`-t`|Número de hilos (default 10, más hilos = más rápido)|
|`-x`|Extensiones a buscar (php, html, txt)|
|`-o`|Guardar resultado en archivo|
|`-s`|Códigos de estado a mostrar|
|`--timeout`|Tiempo límite por petición|

### Ejemplo más completo

```bash
gobuster dir -u http://objetivo.com -w /usr/share/wordlists/dirb/common.txt -t 50 -x php,html,txt -o resultados.txt
```

## Wordlists

Las wordlists son el componente clave, sin una buena lista los resultados serán pobres. Las más usadas vienen en el paquete **SecLists**:

````bash
# En Fedora
sudo dnf install seclists -y

# En Kali
sudo apt install seclists -y
```

Se instalan en `/usr/share/seclists/`. Las más útiles para gobuster:
```
/usr/share/seclists/Discovery/Web-Content/common.txt
/usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt
/usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt
````

## Menús de Ayuda

Cuando realizamos `gobuster --help`, nos aparece lo siguiente en la terminal:

```shell
COMMANDS:  
  dir      Uses directory/file enumeration mode  
  vhost    Uses VHOST enumeration mode (you most probably want to use the IP address as the URL parameter)  
  dns      Uses DNS subdomain enumeration mode  
  fuzz     Uses fuzzing mode. Replaces the keyword FUZZ in the URL, Headers and the request body  
  tftp     Uses TFTP enumeration mode  
  s3       Uses aws bucket enumeration mode  
  gcs      Uses gcs bucket enumeration mode  
  help, h  Shows a list of commands or help for one command  
  
GLOBAL OPTIONS:  
  --help, -h     show help  
  --version, -v  print the version
```


Ahora, si ponemos `gobuster <COMMAND> --help`, siendo `<COMMAND>` alguna de las opciones anteriores, podemos abrir un menú de ayuda por cada comando, por ejemplo, con dns sería:

```shell
gobuster dns --help  
NAME:  
  gobuster dns - Uses DNS subdomain enumeration mode  
  
USAGE:  
  gobuster dns [command options]  
  
OPTIONS:  
  --domain value, --do value            The target domain  
  --check-cname, -c                     Also check CNAME records (default: false)  
  --timeout value, --to value           DNS resolver timeout (default: 1s)  
  --wildcard, --wc                      Force continued operation when wildcard found (default: false)  
  --no-fqdn, --nf                       Do not automatically add a trailing dot to the domain, so the resolver uses the DNS search domai  
n (default: false)  
  --resolver value                      Use custom DNS server (format server.com or server.com:port)  
  --protocol value                      Use either 'udp' or 'tcp' as protocol on the custom resolver (default: "udp")  
  --wordlist value, -w value            Path to the wordlist. Set to - to use STDIN.  
  --delay value, -d value               Time each thread waits between requests (e.g. 1500ms) (default: 0s)  
  --threads value, -t value             Number of concurrent threads (default: 10)  
  --wordlist-offset value, --wo value   Resume from a given position in the wordlist (default: 0)  
  --output value, -o value              Output file to write results to (defaults to stdout)  
  --quiet, -q                           Don't print the banner and other noise (default: false)  
  --no-progress, --np                   Don't display progress (default: false)  
  --no-error, --ne                      Don't display errors (default: false)  
  --pattern value, -p value             File containing replacement patterns  
  --discover-pattern value, --pd value  File containing replacement patterns applied to successful guesses  
  --no-color, --nc                      Disable color output (default: false)  
  --debug                               enable debug output (default: false)  
  --help, -h                            show help
```

