# actualizar-a-Windows11-con-terminal-script

Cómo funciona este método para **actualizar Windows (incluyendo a Windows 11) mediante PowerShell**:

## 📋 Guía completa de PSWindowsUpdate

### **PASO 1: Instalar el módulo**
```powershell
Install-Module -Name PSWindowsUpdate -Force
```
- Descarga e instala el módulo PSWindowsUpdate desde el repositorio oficial de PowerShell
- `-Force` lo instala sin pedir confirmación

### **PASO 2: Verificar instalación**
```powershell
Get-Package -Name PSWindowsUpdate
```
- Confirma que el módulo se instaló correctamente
- Muestra la versión instalada

### **PASO 3: Buscar actualizaciones disponibles**
```powershell
Get-WindowsUpdate
```
- Lista todas las actualizaciones disponibles (Windows Update + Microsoft Update)
- No instala nada, solo muestra qué hay disponible

### **PASO 4: Instalar actualizaciones**

**Opción A - Instalación manual:**
```powershell
Install-WindowsUpdate -MicrosoftUpdate -AcceptAll
```
o
```powershell
Get-WindowsUpdate -AcceptAll -Install
```

**Opción B - Con reinicio automático:**
```powershell
Get-WindowsUpdate -AcceptAll -Install -AutoReboot
```
- `-AcceptAll`: Acepta todas las actualizaciones automáticamente
- `-Install`: Instala las actualizaciones
- `-AutoReboot`: Reinicia el PC automáticamente si es necesario

---

## 🎯 Comandos adicionales útiles:

### **Instalar solo actualizaciones críticas:**
```powershell
Get-WindowsUpdate -AcceptAll -Install -NotCategory "Drivers"
```

### **Ver historial de actualizaciones:**
```powershell
Get-WUHistory
```

### **Desinstalar una actualización:**
```powershell
Remove-WindowsUpdate -KBArticleID KB5034441
```

### **Ocultar una actualización:**
```powershell
Hide-WindowsUpdate -KBArticleID KB5034441
```

---

## ⚠️ Consideraciones importantes:

1. **Requiere PowerShell como Administrador** (clic derecho → "Ejecutar como administrador")

2. **Puede tardar bastante tiempo** dependiendo del número y tamaño de actualizaciones

3. **El `-AutoReboot` reiniciará sin avisar** - guarda tu trabajo antes

4. **Primera vez puede pedir permisos** para instalar desde PSGallery (responde "Sí")

---

## 🚀 Script completo automatizado:

```powershell
# Instalar módulo si no existe
if (-not (Get-Module -ListAvailable -Name PSWindowsUpdate)) {
    Install-Module -Name PSWindowsUpdate -Force -Scope CurrentUser
}

# Importar módulo
Import-Module PSWindowsUpdate

# Mostrar actualizaciones disponibles
Write-Host "Buscando actualizaciones..." -ForegroundColor Cyan
Get-WindowsUpdate

# Instalar todas las actualizaciones
Write-Host "`nInstalando actualizaciones..." -ForegroundColor Green
Get-WindowsUpdate -AcceptAll -Install -AutoReboot
```

Este método es especialmente útil para actualizar **múltiples PCs remotamente** o **automatizar actualizaciones** mediante tareas programadas. 🔧
