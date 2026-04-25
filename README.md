<h1 align="center">Comandos para Windows — Linux — Mac</h1>

## 📑 Índice

- [Windows](#windows)
- [Linux](#linux)
- [Mac](#mac)
- [Otros](#otros)
- [Programas](#programas)
- [Licencia](#licencia)
- [Conclusión](#conclusión)

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

## 💬 Mensajes en pantalla

```bash
cmd /c msg * "Estas siendo revisado"
cmd /c msg %USERNAME% "Hola mundo"
```

---

# 🐧 Linux

## 💬 Mensajes

```bash
zenity --info --text="Estas siendo revisado"
echo "Hola mundo"
```

---

## 📂 Uso de disco

```bash
sudo du -xhd1 /var/lib 2>/dev/null | sort -h
sudo du -xhd1 /var/log 2>/dev/null | sort -h
sudo du -xhd1 /home/worm 2>/dev/null | sort -h
sudo du -xhd1 /usr 2>/dev/null | sort -h
```

---

## 📏 Tamaño de archivos

```bash
ls -lah
```

---

## 🔐 Permisos

```bash
ls -l ruta
ls -ld /home/worm/worm
ls -la /home/worm
```

---

## 📦 Uso real de espacio

```bash
du -sh *
du -sh archivo.log
```

---

# 🍎 Mac

## 💬 Mensajes

```bash
osascript -e 'display dialog "Proceso completado" buttons {"OK"}'
```

---

# ⚙️ Otros

## 🕵️ Procesos

```bash
ps aux | grep -i worm | grep -v grep
ps aux | grep -E "python|WormDefender" | grep -v grep
pgrep -af python
pgrep -af WormDefender
```

### Alternativa más limpia
```bash
pgrep -af python
```

---

## 🔌 Puertos y procesos

```bash
lsof -i :8765
kill -9 PID
```

---

## 📂 Logs y monitoreo

```bash
lsof | grep worm_chain.log
ls -lh /home/worm/worm_chain.log
tail -n 50 /home/worm/worm_chain.log
```

---

## 🌐 Sistema

```bash
df -h
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
```

```bash
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
sudo mkdir -p /etc/apt/keyrings

curl -fsSL https://packages.microsoft.com/keys/microsoft.asc | \
sudo gpg --dearmor -o /etc/apt/keyrings/microsoft.gpg

echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/microsoft.gpg] https://packages.microsoft.com/repos/code stable main" | \
sudo tee /etc/apt/sources.list.d/vscode.list
```

---

# 📜 Licencia

Contenido aquí...

---

# 🧠 Conclusión

Contenido aquí...