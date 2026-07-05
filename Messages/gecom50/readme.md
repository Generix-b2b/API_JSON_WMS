## GECOM50 — Delivery Orders

Mensaje para la creación y mantenimiento de **órdenes de expedición** en el WMS Generix Spain.
Permite crear, modificar o cancelar pedidos de salida de mercancía de forma sincronizada entre el ERP y el WMS.

### Características Principales

- **Operaciones soportadas (TRTEXC):** Creación (`1`), modificación o creación (`2`), modificación de cabecera (`7`) y cancelación (`9`). El valor por defecto es `2`.
- **Identificación del pedido:** La referencia `REFLIV` identifica la orden en el WMS. Los campos `NUMLIV` y `SNULIV` permiten referenciar el número y subnúmero del pedido origen. La cabecera incluye tipo de entrega (`CODTLI`), fecha y hora previstas (`DTILIV`, `HEILIV`), transportista (`CODTRA`), ronda y muelle de expedición (`TOULIV`, `KAILIV`) y mensajes imprimibles en la hoja de preparación y el albarán (`MSGPRP`, `MSGLIV`, hasta 2 líneas cada uno).
- **Tipo de pedido (TYPCDE):** Distingue entre pedido firme (`false`) y provisional (`true`). Los pedidos provisionales no generan preparación hasta su confirmación.
- **Gestión de alcohol (GSTALC):** Configurable a nivel de cabecera: sin gestión (`0`), entrega con DSAC (`1`), entrega con DAC (`2`) o exento de impuestos (`3`).
- **Información adicional de cabecera (GEEX5001):** Fechas de expedición y carga, referencia del pedido del destinatario, código GLN, punto de relevo intermedio (`CLIVIA`), código de anulación y número de gira.
- **Dirección de entrega VPC (GEEX5010):** Bloque opcional con nombre y dirección completa del destinatario final. Permite sobrescribir los datos del maestro para entregas de comercio electrónico o pedidos con dirección ad hoc.
- **Líneas del pedido (GEEX5020):** Array de hasta 99 líneas, cada una con producto (`CODPRO`), cantidad en CSU (`UVCCDE`), lote, sustitución de producto, tipo de operación (promoción/reserva) y marcaje de precio. Requerido cuando `TRTEXC = 1` o `2`.
- **Rubriques:** A nivel de cabecera (`GEEX5005`) y de línea (`GEEX5025`), hasta 99 atributos de trazabilidad por nivel. Las rubriques de línea admiten además rangos de valor mínimo y máximo para control de lote.
- **Texto libre (GEEX5080):** Array de hasta 99 líneas de texto libre impresas en el albarán de entrega (hasta 120 caracteres por línea).

> **Nota importante:** Cuando `TRTEXC = 2` el mensaje reemplaza la ficha completa de la orden, incluyendo todas sus líneas. Para modificar solo la cabecera sin afectar a las líneas existentes, utiliza `TRTEXC = 7`.
>!blue El campo **RCTEXC** es muy importante que este correctamente cumplimentado, para poder redirigir los mensajes a la librería de WMS correcta. La información de este valor es diferente para test y producción, el dato podrá ser proporcionado por el consultor WMS.

### Integración

Este mensaje debe enviarse al WMS **antes** del inicio del proceso de preparación del pedido.
El cliente referenciado en `CODCLI` debe estar previamente declarado mediante **GECOM20**.
Un pedido no declarado impedirá la generación de trabajo de preparación y generará un error de rechazo en el proceso de expedición.
