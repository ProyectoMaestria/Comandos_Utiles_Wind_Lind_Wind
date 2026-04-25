<h1 align="center">Comandos para Windows — Linux — Mac</h1>

## 📑 Índice

- [Windows](#windows)
- [Linux](#linux)
- [Mac](#mac)
- [Otros](#otros)
- [Programas](#programas)
- [Librerias](#librerias)
- [Licencia](#licencia)
- [Conclusión](#conclusión)
Librerias
<h4 align="center">
🚧 Proyecto en construcción 🚧
</h4>

---

# 🪟 Windows

## 🧩 Tareas programadas (schtasks)

### Crear tarea
```bash
schtasks /Create /TN WormDefenderTemp /SC ONCE /ST 23:59 /TR "\"C:\Users\Asus\AppData\Local\Programs\Python\Python312\pythonw.exe\" \"C:\Users\worm\worm\WormDefender.py\"" /F
```

### Ejecutarla
```bash
schtasks /Run /TN WormDefenderTemp
```

### Verificar
```bash
schtasks /Query /TN WormDefenderTemp
```

### Eliminar
```bash
schtasks /delete /tn "WormDefenderTemp" /f
```

---

## 🕵️ Detección de procesos sospechosos

```powershell
Get-CimInstance Win32_Process |
Where-Object { $_.Name -match 'python|powershell|cmd' } |
Select-Object ProcessId, ParentProcessId, Name, CommandLine |
Format-List
```

> ⚠️ **Propósito**  
> Detectar procesos sospechosos, scripts ocultos o identificar quién lanzó qué.

### 🔍 Qué hace

1. Lista todos los procesos en ejecución  
2. Filtra por:
   - python  
   - powershell  
   - cmd  
3. Extrae información relevante  

### 📊 Datos clave

| Campo | Significado |
|------|------------|
| ProcessId | ID del proceso |
| ParentProcessId | Proceso padre (quién lo lanzó) 🔥 |
| Name | Nombre del ejecutable |
| CommandLine | Comando exacto |

---

## 💬 Mensajes en pantalla Windows

```bash
cmd /c msg * "Estas siendo revisados"
cmd /c msg %USERNAME% "Hola mundo"
ejec_com cmd /c msg * %USERNAME%  "Hola mundo"

```

---

# 🐧 Linux

### Usuarios
##Ver si un usuario es admin

```bash
groups usuario
```

## o tambien:
```bash
id usuario
```
## Ver directamente el grupo
```bash
getent group sudo
```
## 👉 Te muestra todos los usuarios con privilegios.

## 🔑 2) Volver admin a un usuario

```bash
sudo adduser nuevo_usuario

```
### Darle Privilegios
```bash

sudo usermod -aG sudo nuevo_usuario
```


##🔑 3) Volver admin a un usuario
```bash
sudo usermod -aG sudo usuario
```
```bash
-a = append (no borra otros grupos)
-G = grupos

⚠️ Luego el usuario debe:

cerrar sesión y volver a entrar
(o ejecutar newgrp sudo, pero mejor relogin limpio)
```

### Bonus, verifica

## Si muestra permisos, es admin
```bash
sudo -l -U usuario
```

```bash

```

## 💬 Mensajes

```bash
zenity --info --text="Estas siendo revisado"
echo "Hola mundo"
```

---

```bash

```

## 🌐 Sistema
### Permite ver el espacio en discos
```bash
df -h
```
---
## 📂 Uso de disco
### Esto permite observar los pesos de los archivos y resolver problemas de disco lleno

```bash
sudo du -xhd1 /var/lib 2>/dev/null | sort -h
sudo du -xhd1 /var/log 2>/dev/null | sort -h
sudo du -xhd1 /home/worm 2>/dev/null | sort -h
sudo du -xhd1 /usr 2>/dev/null | sort -h
```

---

## 📏 Tamaño de archivos
### Ver tamaño legible de archivos
### Puedes usar los comandos ls, du o find. 
###Lista archivos y carpetas del directorio actual.
```bash
ls -lah
```
```bash
🔍 -l (long)

Muestra todo en formato detallado:

permisos (drwxr-xr-x)
número de enlaces
dueño y grupo
tamaño
fecha
nombre
```
```bash
👻 -a (all)

Incluye archivos ocultos.

En Linux, todo lo que empieza con . (como .bashrc) normalmente no se ve.
Con esto, aparece todo.
```
```bash
📏 -h (human)

Hace los tamaños legibles:

1024 → 1K
1048576 → 1M

👉 Nada de números crudos, lo ves claro.

📂 ls -lah

Te muestra los archivos y su tamaño “tal cual” están.
```

👉 Es como pasar de ver nombres… a ver la ficha completa.

### Para ver el tamaño de los archivos en la terminal de Linux: 
### El comando mostrará el tamaño en bytes, 
```bash
ls -l
```
```bash
📂Aquí cambia el juego.

du = disk usage
👉 Mide cuánto espacio REAL están ocupando en disco
```

```bash
🧠 La diferencia que importa

Un archivo puede decir que pesa 1 GB (ls)…
pero en disco puede ocupar:

menos (si está comprimido o sparse)
más (por bloques del sistema de archivos)

Ahí entra du.
```


### Mostrará el tamaño en un formato más legible (MB, GB, etc.), 
```bash
du -h
```

### find puede usarse para buscar archivos por tamaño. 
```bash

```

---

## 🔐 Permisos
### 1. Para ver permisos de una archivo: 
### 2. Para ver permisos de una carpeta:
### 3. Si quieres ver también dueño y grupo de varias cosas:
```bash
ls -l ruta
ls -ld /home/worm/worm
ls -la /home/worm
```
### Para ver cuanto ocupa realmente algo (mucho mejor para carpetas/logs):
```bash
du -sh *
```

### O para algo especifico:
```bash
du -sh archivo.log
```
---

## 📦 Disponible

```bash

```

---

# 🍎 Mac

## 💬 Mensajes

```bash
osascript -e 'display dialog "Proceso completado" buttons {"OK"}'
```

---

# ⚙️ Otros

## Cambiar ip fija en Linux
### Con esto se puede cambiar la ip 

```bash
sudo nano /etc/netplan/01-netcfg.yaml
sudo netplan apply
```

## 🕵️ Procesos
### 👉 Clásico de sysadmin. Aquí ves si tu gusano está vivo… o si hay clones.
```bash
ps aux | grep -i worm | grep -v grep
ps aux | grep -E "python|WormDefender" | grep -v grep
pgrep -af python
pgrep -af WormDefender
```
###  Nota: -i → ignora mayúsculas/minúsculas, Busca cualquier cosa con “worm”

### Alternativa más limpia a la anterior:
### Ejemplo: pgrep -af WormDefender
```bash
pgrep -af python
```
Más elegante que ps + grep.

```bash
pgrep busca procesos directamente
-a → muestra el comando completo
-f → busca en toda la línea de comando
```
---

## 🔌 Puertos y procesos

```bash
lsof -i :8765
kill -9 PID
```
---

## 👉 Esto es más paranoico (bien): detecta nombres ligeramente distintos.
### Aquí ya estás haciendo cirugía.

lsof = lista archivos abiertos por procesos
Filtras por tu log

```bash

lsof | grep worm_chain.log
```

## 📂 Logs y monitoreo
###  Permite leer las 50 primeras lineas
```bash
tail -n 50 /home/worm/worm_chain.log
```

## 📂 Estado del log

### 👉 Si crece demasiado rápido → algo está fuera de control

Tamaño del archivo
Fecha de modificación
```bash
ls -lh /home/worm/worm_chain.log
```
```bash

```

---

## 📡 Copiar por SSH

```bash
scp algoritmo.sh worm@10.11.176.:/home/worm/worm
```

---

## 🔐 Instalar SSH

```bash
sudo apt update
sudo apt install openssh-server

sudo systemctl enable ssh
sudo systemctl start ssh
sudo systemctl status ssh
```

---
## Levantar servidor sencillo python

```bash
python -m http.server 8000
```
## 🐍 Instalar Python 3.12

```bash
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

```

---

## 🧪 Entornos virtuales

```bash
# Windows
gusano\Scripts\activate

# Linux
source gusano/bin/activate
```

---

# 📦 Programas

## Sublime Text

```bash
curl -fsSL https://download.sublimetext.com/sublimehq-pub.gpg | \
gpg --dearmor | sudo tee /usr/share/keyrings/sublimehq-archive.gpg > /dev/null

echo "deb [signed-by=/usr/share/keyrings/sublimehq-archive.gpg] https://download.sublimetext.com/ apt/stable/" | \
sudo tee /etc/apt/sources.list.d/sublime-text.list
```

---

## VS Code

```bash
Pasos: 
1. sudo apt update && sudo apt upgrade -y
2. sudo apt install -y wget gpg
3. wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo install -o root -g root -m 644 microsoft.gpg /usr/share/keyrings/

4. echo "deb [arch=amd64 signed-by=/usr/share/keyrings/microsoft.gpg] https://packages.microsoft.com/repos/code stable main" | sudo tee /etc/apt/sources.list.d/vscode.list
5. sudo apt update
 sudo apt install code

```
## Librerias
### Librerias de desarrollo Linux --- caso cyber

```bash
1. sudo apt update
2. sudo apt install libsystemd-dev
Verificar:
ls /usr/lib/x86_64-linux-gnu/libsystemd.so
```

```bash

```
---

# 📜 Licencia

Contenido aquí...

---

# 🧠 Conclusión

Contenido aquí...