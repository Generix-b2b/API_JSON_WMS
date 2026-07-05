## GECOM51 — Delivery Order Confirmation

Mensaje de **confirmación de expedición** enviado por el WMS Generix Spain al sistema origen (ERP).
Notifica el resultado real de una orden de entrega una vez preparada y expedida: cantidades servidas, soportes preparados y datos de transporte.

### Características Principales

- **Dirección del flujo:** Outbound — el WMS publica este mensaje en el endpoint del cliente (`POST https://[URL_Client]/endpoint`). Es la respuesta al pedido de expedición declarado previamente vía **GECOM50**.
- **Identificación:** La referencia `REFLIV`, junto con el número de orden (`NUMLIV`) y el cliente (`CODCLI`), enlaza la confirmación con el pedido original. El origen se indica en `ORICDE` (interfaz GECOM o entrada local).
- **Liquidación de la entrega (LIVSOL):** Indica si la entrega queda saldada (`true`) o si genera reliquat (`false`). El indicador `INDRLQ` señala la presencia de backorder generado.
- **Información adicional de cabecera (GEEX5101):** Datos de transporte marítimo (barco, naviera, contenedor), transitario, número de expedición y referencias DAE.
- **Dirección de entrega VPC (GEEX5110):** Bloque opcional con la dirección del destinatario final para entregas de comercio electrónico.
- **Líneas entregadas (GEEX5120):** Array de hasta 999 líneas con cantidad pedida (`UVCCDE`), entregada (`UVCLIV`), servida en la ola (`UVCSRV`) e inicialmente pedida (`UVCINI`), más motivos de discrepancia.
- **Detalle por soporte (GEEX5130):** Anidado en cada línea, describe palé, lote, tipo de preparación (picking), datos de mercancías peligrosas, temperatura y números de serie (`GEEX5140`).
- **Totales (GEEX5199):** Resumen con número de líneas, soportes preparados, bultos, productos y pesos bruto y neto de la orden.

> **Nota importante:** Este mensaje es generado por el WMS; el código de proceso `TRTEXC` viene siempre vacío. El ERP debe usar la referencia `REFLIV` para conciliar con el pedido GECOM50 correspondiente.
>!green El campo **RCTEXC** es muy importante que este correctamente cumplimentado, para poder redirigir los mensajes a la librería de WMS correcta. La información de este valor es diferente para test y producción, el dato podrá ser proporcionado por el consultor WMS.

### Integración

El ERP debe mantener un endpoint activo para recibir estas confirmaciones y actualizar el estado de sus pedidos de venta.
Las cantidades servidas y los datos de soporte y transporte permiten al ERP emitir la factura, generar el DESADV al cliente final y cerrar el pedido.
