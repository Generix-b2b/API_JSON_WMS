## GECOM40 — Reception Orders

Mensaje para la creación y mantenimiento de **órdenes de recepción** en el WMS Generix Spain.
Permite crear, modificar o cancelar pedidos de entrada de mercancía de forma sincronizada entre el ERP y el WMS.

### Características Principales

- **Operaciones soportadas (TRTEXC):** Creación (`1`), modificación o creación (`2`), modificación de cabecera (`7`) y cancelación (`9`). El valor por defecto es `2`.
- **Identificación del pedido:** La referencia `REFREC` identifica la orden en el WMS. Los campos `NUMREC` y `SNUREC` permiten referenciar el número y subnúmero del pedido origen.
- **Cabecera:** Incluye proveedor (`CODFOU`), tipo de recepción (`CODTRE`), fecha y hora previstas (`DTIREC`, `HEIREC`), muelle de recepción (`KAIREC`), método de transporte (`METTRP`) y mensaje imprimible en el albarán (`MSGREC`, hasta 2 líneas).
- **Información del proveedor (GEEX4001):** Bloque opcional con nombre, dirección completa y tipo de proveedor. Permite sobrescribir los datos del maestro para esta recepción concreta.
- **Líneas del pedido (GEEX4020):** Array de hasta 99 líneas, cada una con producto (`CODPRO`), cantidad en CSU (`UVCREA`), lote, fechas de fabricación y dimensiones de paletización. Requerido cuando `TRTEXC = 1` o `2`.
- **Números de serie por línea (GEEX4040):** Array anidado en cada línea con hasta 99 números de serie, identificando el tipo (CSU o caja) y el código de palé EAN128.
- **Rubriques:** A nivel de cabecera (`GEEX4005`) y de línea (`GEEX4025`), hasta 99 etiquetas de trazabilidad por nivel.
- **Texto libre (GEEX4080):** Array de hasta 99 líneas de texto libre asociadas al pedido (hasta 120 caracteres por línea).

> **Nota importante:** Cuando `TRTEXC = 2` el mensaje reemplaza la ficha completa de la orden, incluyendo todas sus líneas. Para modificar solo la cabecera sin afectar a las líneas existentes, utiliza `TRTEXC = 7`.
>!green El campo **RCTEXC** es muy importante que este correctamente cumplimentado, para poder redirigir los mensajes a la librería de WMS correcta. La información de este valor es diferente para test y producción, el dato podrá ser proporcionado por el consultor WMS.

### Integración

Este mensaje debe enviarse al WMS **antes** de la llegada física de la mercancía al almacén.
El proveedor referenciado en `CODFOU` debe estar previamente declarado mediante **GECOM10**.
Una orden no declarada impedirá el registro de la recepción y generará un error de rechazo en el proceso de entrada.