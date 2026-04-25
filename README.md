<h1 align="center">Comandos para Windows --- Linux --- Mac</h1>

## Índice

- [Windows](#windows)
- [Linux](#linux)
- [Mac](#mac)
- [Otros](#otros)
- [Disponible](#disponible)
- [Licencia](#licencia)
- [Conclusión](#conclusión)

<h4 align="center">
🚧 Proyecto en construcción 🚧
</h4>

---

## Windows

### Como abrir un cuadro de texto
cmd /c msg * "Estas siendo revisados"

cmd /c msg %USERNAME% "Hola mundo"

ejec_com cmd /c msg * %USERNAME%  "Hola mundo"

## Linux

### Como abrir un cuadro de texto

zenity --info --text="Estas siendo revisados"
echo "Hola mundo"

### Instalar Python3.12
sudo apt update

sudo apt install -y \
build-essential \
wget \
ca-certificates \
zlib1g-dev \
libncurses5-dev \
libgdbm-dev \
libnss3-dev \
libssl-dev \
libreadline-dev \
libffi-dev \
libsqlite3-dev \
libbz2-dev \
liblzma-dev \
tk-dev \
uuid-dev \
xz-utils

cd /usr/src
sudo wget https://www.python.org/ftp/python/3.12.3/Python-3.12.3.tgz
sudo tar -xzf Python-3.12.3.tgz
cd Python-3.12.3

sudo ./configure --enable-optimizations
sudo make -j"$(nproc)"
sudo make altinstall

## Mac

### Como abrir un cuadro de texto
MAC
osascript -e 'display dialog "Proceso completado" buttons {"OK"}'


## Disponible

Contenido aquí...

## Otros

### COmo ver procesos por PID -y Matarlo

lsof -i :8765

kill -9 PID

### Para ver permisos de un archivo o carpeta:

ls -l ruta

### Para ver permisos de una carpeta:

ls -ld /home/worm/worm

### Para ver permisos de un archivo o carpeta:

ls -l ruta

### Si quieres ver también dueño y grupo de varias cosas:

ls -la /home/worm

## Licencia

Contenido aquí...

## Conclusión

Contenido aquí...