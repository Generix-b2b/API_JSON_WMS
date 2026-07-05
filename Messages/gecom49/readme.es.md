## GECOM49 — Dispatch Advice

Mensaje para la declaración de **avisos de expedición (DESADV)** en el WMS Generix Spain.
Permite notificar al almacén el contenido exacto de un envío antes de su llegada física, facilitando la planificación de la recepción.

### Características Principales

- **Operaciones soportadas (TRTEXC):** Creación (`1`), modificación (`2`) y cancelación (`9`). El valor por defecto es `2`.
- **Identificación del aviso:** El campo `AVIREF` es la referencia única del DESADV en el WMS. La cabecera incluye también fecha y hora de expedición (`DATEXP`, `HEUEXP`), fecha y hora de entrega prevista (`DATLIV`, `HEULIV`), número de albarán (`REFLET`), número de camión (`CAMCOD`) y precinto (`REFPLB`).
- **Creación automática de recepción:** El indicador `CRERCP = true` ordena al WMS que genere automáticamente una orden de recepción a partir de este aviso, sin necesidad de enviar un mensaje **GECOM40** independiente.
- **Control de envío parcial (INDSBY):** Permite enviar el aviso en modo retenido (`1`) para completarlo con mensajes sucesivos, y liberarlo con el último envío (`2`).
- **Objetos logísticos (GEEX4910):** Array de hasta 99 palés o bultos, cada uno identificado por su código (`CODOBL`) y número de línea (`AVINLI`). Incluye peso, dimensiones, tipo de marcaje y códigos de embalaje. Requerido cuando `TRTEXC = 1` o `2`.
- **Detalle del objeto logístico:** Cada objeto logístico contiene subbloques anidados con el producto y lote (`GEEX4920`, requerido), datos de fabricación y referencia de recepción (`GEEX4921`), referencia de entrega y precio (`GEEX4922`), y datos de promoción o inmobilización (`GEEX4923`).
- **Rubriques:** A nivel de cabecera (`GEEX4905`) y de objeto logístico (`GEEX4925`), hasta 99 atributos de trazabilidad por nivel.

> **Nota importante:** A diferencia de **GECOM40**, el modelo de GECOM49 organiza la mercancía por objetos logísticos (palés, bultos), no por líneas de producto. El producto y la cantidad se declaran dentro del subbloque `GEEX4920` de cada objeto.
>!blue El campo **RCTEXC** es muy importante que este correctamente cumplimentado, para poder redirigir los mensajes a la librería de WMS correcta. La información de este valor es diferente para test y producción, el dato podrá ser proporcionado por el consultor WMS.

### Integración

Este mensaje debe enviarse al WMS **antes** de la llegada física del camión al almacén.
El proveedor referenciado en `CODFOU` debe estar previamente declarado mediante **GECOM10**.
Si `CRERCP = false`, la orden de recepción correspondiente debe existir en el WMS (declarada vía **GECOM40**) para que el aviso pueda asociarse correctamente.