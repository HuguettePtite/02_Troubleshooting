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
