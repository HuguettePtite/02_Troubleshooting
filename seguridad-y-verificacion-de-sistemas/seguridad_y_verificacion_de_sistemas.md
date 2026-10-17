# Guía Breve: Verificación y Diagnóstico de Seguridad en Windows y WSL (Linux)

Este documento resume los comandos y conceptos clave utilizados para analizar la seguridad de un equipo, verificar procesos activos y descartar amenazas tras interactuar con posibles sitios engañosos o de ingeniería social.

---

## 1. Verificación en Windows (PowerShell)

Para comprobar el estado del sistema anfitrión, siempre se recomienda ejecutar **PowerShell como Administrador**.

### Comandos Clave:

* **Conexiones de red activas y sus procesos:**
  ```powershell
  Get-NetTCPConnection -State Establish | Select-Object LocalAddress, LocalPort, RemoteAddress, RemotePort, OwningProcess, @{Name="ProcessName";Expression={(Get-Process -Id $_.OwningProcess).ProcessName}} | Format-Table -AutoSize
  ```
  * **Objetivo:** Identificar qué programas están conectados a internet en tiempo real y descartar ejecutables no reconocidos.

* **Programas en el inicio del sistema (Persistencia):**
  ```powershell
  Get-CimInstance Win32_StartupCommand | Select-Object Name, Command, Location, User | Format-Table -AutoSize
  ```
  * **Objetivo:** Verificar que no haya scripts o aplicaciones sospechosas configuradas para ejecutarse al encender el equipo.

* **Análisis rápido de antivirus (Windows Defender):**
  ```powershell
  Start-MpScan -ScanType QuickScan
  ```
  * **Objetivo:** Activar el motor nativo de escaneo en segundo plano.

---

## 2. Verificación en WSL / Ubuntu (Linux)

Cuando se trabaja con Subsystem for Linux (WSL), es útil revisar las interfaces internas de red y la tabla de procesos.

### Comandos Clave:

* **Puertos en escucha y sockets de red:**
  ```bash
  sudo ss -tulpn
  ```
  * **Objetivo:** Muestra qué servicios tienen puertos abiertos. Usar `sudo` permite visualizar la columna `Process` con el nombre del ejecutable.

* **Monitoreo de procesos y uso de CPU:**
  ```bash
  ps aux --sort=-%cpu | head -n 10
  ```
  * **Objetivo:** Listar los 10 procesos que consumen más recursos para detectar minadores o scripts ocultos.

* **Revisión de tareas programadas en fondo:**
  ```bash
  crontab -l
  ```
  * **Objetivo:** Confirmar que no existan tareas automáticas maliciosas configuradas en el entorno del usuario.

---

## 3. Conceptos Técnicos Aprendidos

### Sockets UDP y el estado `UNCONN`
* **`UNCONN` (Unconnected):** Es un estado completamente normal para el protocolo **UDP**. A diferencia de TCP, UDP no establece conexiones permanentes. Indica que el socket está en escucha pasiva.
* **Puertos del sistema comunes en WSL:**
  * `127.0.0.53` / `127.0.0.54` / `10.255.255.254` (Puerto 53): Servicio `systemd-resolved` para resolución de nombres DNS.
  * `127.0.0.1:323` (Puerto 323): Servicio `chrony` o `systemd-timesyncd` para sincronización de tiempo NTP con Windows.

### Procesos Base del Sistema
* **`root` / `syslog`:** Procesos nativos del Kernel de Linux y del sistema de registro de eventos.
* **Procesos de usuario:** Muestran únicamente la interacción directa del usuario en la shell (ej. `bash`, `ps`).

---

## 4. Puntos de Seguridad en Phishing y Fraude Digital

1. **Pasarelas de Pago vs. Vendedores:**
   * Un correo legítimo de una plataforma de pago (como `info@mercadopago.com`) solo garantiza que la transacción fue generada en su sistema.
   * La plataforma de pago no valida la autenticidad ni la existencia del evento vendido por un tercero.
2. **Estrategia de Pagos en Efectivo (OXXO/SPEI):**
   * Generar una ficha de pago temporal permite revisar el evento sin exponer datos bancarios ni realizar el desembolso.
3. **Ataques de Ingeniería Social vs. Malware:**
   * La mayoría de las estafas en redes buscan la entrega voluntaria de dinero a través de urgencia simulada, no infectar la computadora con virus.