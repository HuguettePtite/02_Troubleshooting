# Incidente: Mitigación de Browser Hijacker y Persistencia de Software PUP (McAfee)
***Descripción del Problema*** Se detectó la persistencia de un motor de búsqueda no deseado (Yahoo) en la barra de direcciones (Omnibox) de Google Chrome. El síntoma persistía incluso tras el cambio manual de configuración, activándose específicamente al abrir nuevas pestañas o interactuar con la barra de URL.

***Origen Identificado*** El secuestro del navegador (Browser Hijacking) fue originado por una extensión residual de McAfee WebAdvisor, instalada posiblemente mediante tácticas de bundling o redirecciones forzadas durante procesos de desuscripción de plataformas externas.

## Metodología de Resolución (IR - Incident Response):

Identificación de Persistencia en Navegador:

- Se eliminaron extensiones no autorizadas en chrome://extensions/.

- Se ejecutó un Reset de la configuración de Chrome para limpiar el caché de redirecciones y motores de búsqueda predeterminados.

## Análisis de Procesos en Tiempo Real (PowerShell):

Uso de Get-Process con filtros de búsqueda para asegurar que no existieran binarios de McAfee activos en memoria.

```powershell
Get-Process | Where-Object {$_.ProcessName -like "*McAfee*"}
```

## Auditoría de Integridad del Sistema:

Ejecución de sfc /scannow para verificar archivos protegidos del sistema operativo.

Escaneo con Microsoft Defender para descartar amenazas de mayor criticidad (Malware/Trojan).

## Eliminación de Artefactos Residuales (Limpieza de Directorios):

Se identificaron carpetas persistentes en rutas críticas utilizando variables de entorno:

```powershell 
$env:ProgramData\McAfee
$env:LOCALAPPDATA\McAfee
```

## Se procedió a la eliminación forzosa mediante PowerShell:

```powershell
Remove-Item -Path "$env:ProgramData\McAfee" -Recurse -Force
Remove-Item -Path "$env:LOCALAPPDATA\McAfee" -Recurse -Force
```

### 2. Estructura con comentarios explicativos

```powershell
# 1. Verificar si existen procesos activos en memoria
Get-Process | Where-Object {$_.ProcessName -like "*McAfee*"}

# 2. Validar existencia de directorios residuales en perfiles de usuario y sistema
Test-Path "$env:ProgramData\McAfee"; Test-Path "$env:LOCALAPPDATA\McAfee"

# 3. Eliminación forzosa de persistencias detectadas
Remove-Item -Path "$env:ProgramData\McAfee" -Recurse -Force -ErrorAction SilentlyContinue
```

### Análisis de Parámetros de Mitigación

| Parámetro | Función Técnica | Alineación |
| :--- | :--- | :---: |
| `-Recurse` | Indica al comando que debe procesar y borrar todos los subdirectorios y archivos de forma descendente dentro de la ruta especificada. | ⬅️ |
| `-Force` | Permite la eliminación de archivos que normalmente no se pueden modificar, omitiendo restricciones de seguridad menores como el atributo de solo lectura. | ⬅️ |
| `-ErrorAction` |Define cómo debe reaccionar el script ante un fallo; en este caso, evita que se detenga o muestre mensajes de error si la carpeta ya no existe. | ⬅️ |

## Lecciones Aprendidas:

- La desinstalación estándar de software de terceros (Bloatware/Antivirus) no garantiza la eliminación de extensiones en navegadores.

- Los procesos de desuscripción de redes sociales pueden emplear Dark Patterns para forzar la instalación de PUPs (Potentially Unwanted Programs).

- La verificación manual de rutas de datos (AppData y ProgramData) es esencial para asegurar la erradicación total de persistencias.

