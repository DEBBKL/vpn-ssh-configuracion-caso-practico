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
