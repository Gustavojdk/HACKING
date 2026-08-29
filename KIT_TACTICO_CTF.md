# Kit Táctico de Terminal para CTF en Debian

Guía rápida de herramientas habituales para resolver retos de imágenes, esteganografía, análisis forense, reversing y OSINT desde Debian.

## Índice

- [Visualizadores de imágenes en terminal](#visualizadores-de-imágenes-en-terminal)
  - [Catimg](#catimg)
  - [Fim](#fim)
- [Esteganografía y análisis de imágenes](#esteganografía-y-análisis-de-imágenes)
  - [Steghide](#steghide)
  - [Zsteg](#zsteg)
  - [Binwalk](#binwalk)
  - [ImageMagick](#imagemagick)
- [Forense y misceláneo](#forense-y-misceláneo)
  - [File y Stat](#file-y-stat)
  - [Xxd y Hexdump](#xxd-y-hexdump)
  - [Strings](#strings)
  - [Foremost](#foremost)
- [Reversing (ingeniería inversa)](#reversing-ingeniería-inversa)
  - [Radare2](#radare2)
  - [Ghidra](#ghidra)
  - [Ltrace y Strace](#ltrace-y-strace)
  - [Checksec](#checksec)
- [OSINT (investigación)](#osint-investigación)
  - [Exiftool](#exiftool)
  - [Sherlock](#sherlock)
  - [TheHarvester](#theharvester)

---

## Visualizadores de imágenes en terminal

### Catimg

**Qué es:** Renderiza imágenes en color real directamente en la consola usando caracteres Unicode.

**Comando de uso:**

```bash
catimg imagen.png
```

**Comando de instalación:**

```bash
sudo apt install catimg
```

### Fim

**Qué es:** Visor de imágenes ultraligero que funciona por framebuffer o entorno gráfico básico.

**Comando de uso:**

```bash
fim imagen.jpg
```

**Comando de instalación:**

```bash
sudo apt install fim
```

**Nota:** `fim` puede requerir acceso al framebuffer o una configuración gráfica compatible.

---

## Esteganografía y análisis de imágenes

### Steghide

**Qué es:** Oculta y extrae datos binarios dentro de imágenes JPG y BMP.

**Comando de uso:**

```bash
steghide info imagen.jpg
steghide extract -sf imagen.jpg
```

**Comando de instalación:**

```bash
sudo apt install steghide
```

### Zsteg

**Qué es:** Analiza canales LSB (Least Significant Bit), especialmente en formatos PNG y BMP.

**Comando de uso:**

```bash
zsteg -a imagen.png
```

**Comando de instalación:**

```bash
sudo apt install ruby ruby-dev build-essential
sudo gem install zsteg
```

### Binwalk

**Qué es:** Detecta y extrae archivos ocultos, comprimidos o concatenados dentro de binarios e imágenes.

**Comandos de uso:**

```bash
# Escanear un archivo
binwalk imagen.png

# Extraer los archivos detectados
binwalk -e imagen.png
```

**Comando de instalación:**

```bash
sudo apt install binwalk
```

### ImageMagick

**Qué es:** Suite para manipular imágenes; resulta útil, entre otras tareas, para voltearlas cuando contienen texto especular, al estilo Da Vinci.

**Comandos de uso:**

```bash
# Espejo horizontal
convert imagen.png -flop salida.png

# Espejo vertical
convert imagen.png -flip salida.png
```

**Comando de instalación:**

```bash
sudo apt install imagemagick
```

**Nota:** En versiones recientes de ImageMagick también puede utilizarse `magick` en lugar de `convert`.

---

## Forense y misceláneo

### File y Stat

**Qué es:** `file` identifica el formato real de un archivo ignorando su extensión, mientras que `stat` muestra sus propiedades y metadatos del sistema de archivos.

**Comandos de uso:**

```bash
file archivo_misterioso
stat archivo_misterioso
```

**Comando de instalación:**

```bash
sudo apt install file
```

**Nota:** `stat` forma parte de las utilidades básicas del sistema en Debian y normalmente ya está instalado junto con ellas.

### Xxd y Hexdump

**Qué es:** Inspectores de bytes en formato hexadecimal y ASCII, ideales para revisar magic numbers.

**Comando de uso:**

```bash
xxd archivo | head -n 20
```

**Comando de instalación:**

```bash
sudo apt install bsdmainutils
```

**Nota:** En algunas versiones actuales de Debian, `xxd` se distribuye junto con Vim y `hexdump` con el paquete `bsdextrautils`.

### Strings

**Qué es:** Extrae cadenas de texto imprimibles de archivos binarios.

**Comando de uso:**

```bash
strings imagen.jpg | grep -iE "flag|ctf|{"
```

**Comando de instalación:**

```bash
sudo apt install binutils
```

### Foremost

**Qué es:** Herramienta de tallado (carving) para recuperar archivos ocultos a partir de sus cabeceras.

**Comando de uso:**

```bash
foremost -i imagen.png -o carpeta_salida/
```

**Comando de instalación:**

```bash
sudo apt install foremost
```

---

## Reversing (ingeniería inversa)

### Radare2

**Qué es:** Framework de análisis y desensamblado interactivo desde la terminal.

**Comando de uso:**

```bash
r2 binario
```

En la interfaz de `r2`, presiona `V` para entrar en modo visual y `p` para cambiar de vista.

**Comando de instalación:**

```bash
sudo apt install radare2
```

### Ghidra

**Qué es:** Descompilador avanzado que traduce binarios a código similar a C.

**Comando de uso:**

Ejecuta la interfaz gráfica, crea un proyecto e importa el binario que quieras analizar.

**Comando de instalación:**

```bash
sudo apt install ghidra default-jdk
```

**Nota:** Ghidra necesita un entorno gráfico y una versión de Java compatible.

### Ltrace y Strace

**Qué es:** `ltrace` rastrea llamadas a bibliotecas y `strace` rastrea llamadas al sistema durante la ejecución.

**Comandos de uso:**

```bash
ltrace ./programa
strace ./programa
```

**Comando de instalación:**

```bash
sudo apt install ltrace strace
```

### Checksec

**Qué es:** Evalúa las protecciones y mitigaciones de seguridad activas de un binario, como NX, Canary y PIE.

**Comando de uso:**

```bash
checksec --file=binario
```

**Comando de instalación:**

```bash
sudo apt install checksec
```

---

## OSINT (investigación)

### Exiftool

**Qué es:** Lee y escribe metadatos detallados, como fechas, coordenadas GPS y datos de cámaras, en archivos multimedia.

**Comando de uso:**

```bash
exiftool foto.jpg
```

**Comando de instalación:**

```bash
sudo apt install libimage-exiftool-perl
```

### Sherlock

**Qué es:** Rastrea cuentas de usuario en cientos de redes sociales de forma automatizada.

**Comando de uso:**

```bash
sherlock nombre_usuario
```

**Comando de instalación:**

```bash
sudo apt install python3-pip
pip3 install sherlock-project
```

**Nota:** Considera usar un entorno virtual de Python para evitar mezclar dependencias del sistema con las del proyecto.

### TheHarvester

**Qué es:** Recopila correos electrónicos, subdominios y nombres asociados a un dominio o empresa.

**Comando de uso:**

```bash
theharvester -d dominio.com -b all
```

**Comando de instalación:**

```bash
sudo apt install theharvester
```
