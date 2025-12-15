# HOLA, ME LLAMO HUGUETTE

**Soy Desarrolladora de Software con un perfil versátil que abarca múltiples dominios:** Desarrollo Frontend, Administración de TI y Análisis de Ciberseguridad.

Me enfoco en la **optimización de rendimiento** y la creación de **infraestructura robusta**. Mis habilidades me permiten trabajar en todo el ciclo de vida del software, con especial atención a la seguridad y la experiencia:

* **Desarrollo Frontend:** Expertise en el ciclo completo de desarrollo, desde el diseño de la interfaz de usuario hasta el código **HTML, CSS y JavaScript** (ver carpeta `01_Frontend`).
* **Diagnóstico de Hardware:** Sólida habilidad de **diagnóstico y solución de problemas críticos de hardware/sistema** (ver `02_Troubleshooting`).
* **Seguridad (Próximo):** Monitoreo activo de posibles riesgos de interfaces de usuario y **análisis de vulnerabilidades** web (ver carpeta `03_Ciberseguridad`).


Mi principal enfoque es la **optimización del rendimiento** y la creación de **infraestructura robusta**. Mis habilidades me permiten trabajar en todo el ciclo de vida del software, desde la experiencia de usuario (`01_Frontend`) hasta la gestión y seguridad de sistemas operativos.

Destaco mi sólida habilidad para el diagnóstico y solución de problemas críticos de hardware/sistema (ver `02_Troubleshooting`) y la aplicación de políticas de seguridad en la administración de redes y sistemas (`03_Ciberseguridad`).

# 📂 Diagnóstico de Falla de GPU - HP Pavilion dv5-1135la (2008)

## Resumen del Caso y Conclusión Final

Este repositorio documenta el diagnóstico de una laptop HP Pavilion dv5-1135la con síntoma de "pantalla negra" (sin imagen en ningún momento del arranque).

### 🛠️ Flujo de Diagnóstico y Resultados

| Paso de Diagnóstico | Acción Realizada | Resultado | Conclusión / Descarte |
| :--- | :--- | :--- | :--- |
| **1. Verificación Inicial** | Confirmación de LEDs y Ventilador. | Ventilador y LEDs de encendido/función **ACTIVOS**. | Descarta una falla total de fuente de alimentación o placa base en etapa inicial. |
| **2. Prueba de Salida Externa (VGA)** | Conexión a un Monitor externo por VGA. | **Sin imagen** en el monitor externo. | Descarta falla del cable flexible o retroiluminación interna. |
| **3. Prueba de Salida Externa (HDMI)** | Conexión a un Proyector por HDMI (usando adaptador). | **Sin imagen** en el proyector. | **Confirma** que la unidad generadora de video (GPU) está fallando. |
| **4. Diagnóstico Final** | No hay pitidos de error de BIOS (POST). | El sistema inicia, pero no emite señal de video en ninguna salida. | **Falla Crítica de Hardware:** El chip GPU ATI Radeon HD 3450 ha fallado (típico *cold solder joint* en esta serie). |

---

### 📦 Componentes Rescatados (Inventario de Piezas)

| Componente | Especificaciones | Estado / Uso |
| :--- | :--- | :--- |
| **Disco Duro (HDD)** | 320 GB SATA 5400 RPM | **Funcional.** Destinado a almacenamiento externo con un *caddy* USB. |
| **Memoria RAM** | 3072 MB (aprox.) DDR2 800MHz | **Funcional.** Se puede usar para diagnosticar otras PC antiguas o para reventa. |
| **Tarjeta Gráfica (GPU)** | ATI Radeon HD 3450 | **Fallida (Fallo de Soldadura).** No recuperable. |
| **Cargador AC** | Genérico / No original | **Funcional (pero de baja calidad).** Útil solo para pruebas. |
| **Pantalla LCD** | Desconocido | **Potencialmente funcional.** El panel podría usarse en un proyecto de monitor secundario. |