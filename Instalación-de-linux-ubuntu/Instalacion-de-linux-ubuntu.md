# 🐧 Bitácora de Instalación Dual Boot: Windows + Ubuntu 24.04 LTS

Documentación del proceso de configuración e instalación paso a paso de un entorno de arranque dual (**Dual Boot**) con **Windows** y **Ubuntu Linux** en una laptop con hardware clásico.

---

## 📌 1. Especificaciones del Hardware

* **Equipo:** Laptop ASUS
* **Procesador:** Intel® Pentium® N4200 (1.10 GHz)
* **Memoria RAM:** 4 GB
* **Almacenamiento:** HDD 1 TB (Serial ATA HGST 7200 RPM)
* **Firmware:** ASUS BIOS Utility - EZ Mode (UEFI Version 303)

---

## 🛠️ 2. Preparación del Sistema y Medios de Instalación

### A. Preparación de la Memoria Booteable
1. Se descargó la imagen ISO oficial de **Ubuntu LTS**.
2. Se utilizó la herramienta **Rufus** para flashear la imagen en una memoria USB **Kingston DataTraveler 3.0**.
3. **Configuración de Rufus:**
   * **Esquema de partición:** GPT / UEFI.
   * **Tamaño de clúster:** 32 KB (por defecto).

### B. Particionamiento del Disco en Windows
1. Se accedió a la herramienta **Administración de discos** (`diskmgmt.msc`) en Windows.
2. Se realizó una reducción del volumen principal **(C:)** en `102,400 MB` (**~100 GB**).
3. Se generó un espacio libre **"No asignado"** en el disco duro, reservado exclusivamente para la raíz e instalación de Ubuntu, preservando intacta la partición de Windows (~892 GB).

---

## ⚙️ 3. Configuración de Firmware (BIOS/UEFI)

1. Se insertó el medio de instalación en el puerto USB.
2. Se accedió a la BIOS del sistema mediante la tecla **F2 / F8** durante el arranque.
3. En el apartado **Boot Priority**, se ajustó el orden de arranque para priorizar el dispositivo `UEFI: KingstonDataTraveler Partition 1`.
4. Se guardaron los cambios y se reinició el equipo (`F10`).

---

## 🚀 4. Proceso de Instalación de Ubuntu

1. **Gestor de arranque GRUB:** Se seleccionó la opción `Try or Install Ubuntu`.
2. **Asistente de instalación:**
   * **Idioma:** Español / Español (Latinoamérica) para el teclado.
   * **Conexión a red:** Configuración Wi-Fi activa para la descarga de controladores propietarios y códecs de medios de terceros.
   * **Tipo de instalación:** *Instalación interactiva* y *Sin cifrado* de disco.
   * **Asignación de espacio:** Se seleccionó la opción **"Instalar Ubuntu junto a Windows Boot Manager"**. El instalador detectó automáticamente el espacio no asignado de 100 GB para montar las particiones raíz (`/`) y SWAP, manteniendo las particiones `Basic data partition` y `Windows Boot Manager` sin modificar.

---

## 📝 5. Aprendizajes y Consideraciones Técnicas

* **Gestión de almacenamiento en Linux:** En el entorno gráfico de Ubuntu, la partición principal de Windows aparece reflejada en la barra lateral como un volumen independiente (e.g. *Volumen de 892 GB*). Esto permite el acceso de lectura a los archivos almacenados en NTFS desde Linux sin comprometer la integridad del sistema operativo anfitrión.
* **Tiempos de escritura en discos HDD:** Debido al uso de almacenamiento mecánico (HDD de 7200 RPM) y un procesador de bajo consumo, el desempacado e instalación de paquetes requirió un tiempo prolongado (~35–45 min), lo cual es el comportamiento esperado en este tipo de arquitectura de hardware.
* **Arranque Dual (GRUB):** La instalación configura el gestor de arranque GRUB de forma automática en la partición EFI, permitiendo elegir entre **Ubuntu** y **Windows Boot Manager** al momento de encender el equipo.

---

*Desarrollado y documentado para la clase de sistemas operativos y desarrollo.*