<h1 align="center">Comandos para Windows --- Linux --- Mac</h1>

## Índice

- [Windows](#windows)
- [Linux](#linux)
- [Mac](#mac)
- [Otros](#otros)
- [Programas_Linux](#programas)
- [Licencia](#licencia)
- [Conclusión](#conclusión)

<h4 align="center">
🚧 Proyecto en construcción 🚧
</h4>

---

## Windows

### Crear tarea y programarla en Windows

#### Crear tarea

schtasks /Create /TN WormDefenderTemp /SC ONCE /ST 23:59 /TR "\"C:\Users\Asus\AppData\Local\Programs\Python\Python312\pythonw.exe\" \"C:\Users\worm\worm\WormDefender.py\"" /F

#### Ejecutarla ya

schtasks /Run /TN WormDefenderTemp

#### Verificar

schtasks /Query /TN WormDefenderTemp

#### Eliminar

schtasks /delete /tn "WormDefenderTemp" /f

### Sirve para detectar Scripts o procesos sospechosos o quien lazo q cosa, o procesos ocultos
Descripcion por linea: 1. Le pide a Windows la lista completa de procesos en ejecución.
Es como abrir el “Administrador de tareas”, pero con rayos X: te da más detalle interno.
2.Filtra solo los procesos cuyo nombre coincida con:

python
powershell
cmd

Ese -match usa regex, así que encuentra cualquier cosa que contenga esas palabras.
3. De esos procesos, saca datos clave:

ProcessId → el ID del proceso
ParentProcessId → quién lo lanzó (esto es oro puro 🔥)
Name → nombre del ejecutable
CommandLine → el comando exacto con el que se inició

4. Lo muestra en formato lista, bonito y legible (no en tabla apretada).

Get-CimInstance Win32_Process |
Where-Object { $_.Name -match 'python|powershell|cmd' } |
Select-Object ProcessId, ParentProcessId, Name, CommandLine |
Format-List




### Como abrir un cuadro de texto
cmd /c msg * "Estas siendo revisados"

cmd /c msg %USERNAME% "Hola mundo"

ejec_com cmd /c msg * %USERNAME%  "Hola mundo"

## Linux

### Como abrir un cuadro de texto

zenity --info --text="Estas siendo revisados"
echo "Hola mundo"

### Revisar archivos pesados Linux

sudo du -xhd1 /var/lib 2>/dev/null | sort -h
sudo du -xhd1 /var/log 2>/dev/null | sort -h
sudo du -xhd1 /home/worm 2>/dev/null | sort -h
sudo du -xhd1 /usr 2>/dev/null | sort -h

### Ver tamaño legible de archivos

ls -lah  Para ver mas en formato humano

### Para ver permisos de un archivo o carpeta:

ls -l ruta

### Para ver permisos de una carpeta:

ls -ld /home/worm/worm

### Para ver permisos de un archivo o carpeta:

ls -l ruta

### Si quieres ver también dueño y grupo de varias cosas:

ls -la /home/worm

### Para ver cuanto ocupa realmente algo (mucho mejor para carpetas/logs):

du -sh *

### O para algo especifico:

du -sh archivo.log

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

### Copiar algo mediante ssh

scp algoritmo.sh worm@10.11.176.:/home/worm/worm

###  Revisar en linux procesos
2. Procesos en ejecución (la cacería)
Lista todos los procesos
Filtra los que tengan python o WormDefender
Quita el propio grep para no contaminar

👉 Clásico de sysadmin. Aquí ves si tu gusano está vivo… o si hay clones.

ps aux | grep -i worm | grep -v grep

Versión más general:

-i → ignora mayúsculas/minúsculas
Busca cualquier cosa con “worm”

👉 Esto es más paranoico (bien): detecta nombres ligeramente distintos.

lsof | grep worm_chain.log

Aquí ya estás haciendo cirugía.

lsof = lista archivos abiertos por procesos
Filtras por tu log

📂 Estado del log
ls -lh /home/worm/worm_chain.log
Tamaño del archivo
Fecha de modificación

👉 Si crece demasiado rápido → algo está fuera de control


df -h
ps aux | grep -E "python|WormDefender" | grep -v grep
pgrep -af python
lsof | grep worm_chain.log
ls -lh /home/worm/worm_chain.log
tail -n 50 /home/worm/worm_chain.log


ps aux | grep -i worm | grep -v grep
ps aux | grep -E "python|WormDefender" | grep -v grep
pgrep -af WormDefender
pgrep -af python



lsof | grep worm_chain.log

### Mas elegante q ps + grep

pgrep -af python

Más elegante que ps + grep.

pgrep busca procesos directamente
-a → muestra el comando completo
-f → busca en toda la línea de comando

### Instalar ssh Linux

1.
sudo apt update
sudo apt install openssh-server

2.
sudo systemctl enable ssh
sudo systemctl start ssh

3.
sudo systemctl status ssh


### Instalar Python3.12 Linux
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


#### Ambientes virtuales python
PARA WINDOWS: gusano\Scripts\activate

PARA LINUX: source gusano/bin/activate

gusano\Scripts\activate


## Programa
### Instalacion Programas

#### Instalar sublime text

curl -fsSL https://download.sublimetext.com/sublimehq-pub.gpg | \
gpg --dearmor | sudo tee /usr/share/keyrings/sublimehq-archive.gpg > /dev/null


echo "deb [signed-by=/usr/share/keyrings/sublimehq-archive.gpg] https://download.sublimetext.com/ apt/stable/" | \
sudo tee /etc/apt/sources.list.d/sublime-text.list


#### Instalar code

wget -qO- https://packages.microsoft.com/keys/microsoft.asc | \
gpg --dearmor | sudo tee /usr/share/keyrings/microsoft.gpg > /dev/null

echo "deb [arch=amd64 signed-by=/usr/share/keyrings/microsoft.gpg] https://packages.microsoft.com/repos/code stable main" | \
sudo tee /etc/apt/sources.list.d/vscode.list

sudo rm -f /etc/apt/sources.list.d/vscode.list
sudo rm -f /usr/share/keyrings/microsoft.gpg

sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://packages.microsoft.com/keys/microsoft.asc | \
sudo gpg --dearmor -o /etc/apt/keyrings/microsoft.gpg

echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/microsoft.gpg] https://packages.microsoft.com/repos/code stable main" | \
sudo tee /etc/apt/sources.list.d/vscode.list




## Licencia

Contenido aquí...

## Conclusión

Contenido aquí...