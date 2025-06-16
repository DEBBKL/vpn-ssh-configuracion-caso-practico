# Caso práctico: Configuración de acceso remoto VPN mediante SSH

## 🗂️ Escenario

El administrador de red necesita poner a disposición un archivo de configuración VPN para que los empleados puedan descargarlo desde sus casas. El acceso se realiza vía SSH a un servidor Windows 11 dentro de la red corporativa.

---

## 🔐 Paso 1: Habilitar el puerto 22

Antes de instalar cualquier servicio, es vital permitir conexiones entrantes por el puerto 22 en el firewall de Windows:

1. Crear reglas de entrada y salida para permitir el tráfico TCP por el puerto 22.
2. Verificar que no haya restricciones adicionales (antivirus o políticas de grupo).

---

## 🧰 Paso 2: Instalación del servidor SSH en Windows 11

### Opción gráfica:
1. Ir a **Configuración > Aplicaciones > Características opcionales**.
2. Clic en **Agregar una característica**.
3. Buscar y seleccionar **Servidor OpenSSH**, luego clic en **Instalar**.

### Opción PowerShell:

```powershell
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
```

---

## ⚙️ Paso 3: Configurar y activar el servicio

### Iniciar el servicio:

```powershell
Start-Service sshd
```

### Configurar inicio automático:

```powershell
Set-Service -Name sshd -StartupType Automatic

### Verificar que el puerto 22 está escuchando:

```powershell
netstat -an | findstr :22
```

---

## 👥 Paso 4: Configuración del usuario

- Crear o utilizar una cuenta estándar (no administrador).
- Asegurarse de que tenga contraseña definida.
- Iniciar sesión como ese usuario (ej: RISTOMEJIDE).

---

## 🖥️ Paso 5: Prueba de conexión desde cliente (Kali Linux)

IPs de ejemplo:
- Windows 11: 10.0.2.15
- Kali Linux: 10.0.2.5

Comando para conectarse desde Kali:

```bash
ssh RISTOMEJIDE@10.0.2.15
```

---

## 📤 Paso 6: Transferencia de archivos

Desde Kali, el empleado puede descargar el archivo de configuración VPN con:

```bash
scp RISTOMEJIDE@10.0.2.15:/ruta/al/archivo.ovpn ~/Descargas/
```

---

## 🔐 Seguridad adicional

- Añadir clave pública del usuario cliente en ~/.ssh/authorized_keys del servidor.
- Usar archivo ~/.ssh/config para definir alias SSH en cliente.
- Configurar acceso restringido por IP o grupo.

## ✅ Conclusión

Este caso práctico demuestra la implementación de un acceso remoto seguro para la distribución de un archivo de configuración VPN en un entorno Windows + Linux mediante SSH. Refleja buenas prácticas de seguridad y administración de sistemas.
