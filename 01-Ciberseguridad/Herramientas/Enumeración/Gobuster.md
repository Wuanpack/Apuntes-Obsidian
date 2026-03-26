---
tags:
  - herramientas/enumeracion
---

## ¿Qué es?

Gobuster es una herramienta de seguridad de código abierto escrita en Go, utilizada para la fuerza bruta en servidores web mediante técnicas de [[Enumeración]] rápida. Es ampliamente utilizada por pentesters para el reconocimiento en auditorías de seguridad web.

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

**dir** — busca directorios y archivos ocultos:


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