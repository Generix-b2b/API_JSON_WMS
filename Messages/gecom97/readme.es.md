## GECOM97 — Status Orders

Mensaje de **notificación de estado** de órdenes de recepción y expedición enviado por el WMS Generix Spain al sistema origen (ERP).
Informa en tiempo real de los cambios de estado que se producen en el almacén durante el ciclo de vida de un pedido.

### Características Principales

- **Dirección del flujo:** Outbound — el WMS publica este mensaje en el endpoint del cliente (`POST https://[URL_Client]/endpoint`). El ERP debe exponerlo y procesarlo.
- **Operaciones soportadas (TRTEXC):** Modificación o creación (`2`). El valor por defecto es `2`.
- **Metadatos de intercambio:** Cada registro incluye emisor (`EMTEXC`), receptor (`RCTEXC`), fecha (`DATEXC`) y hora (`HEUEXC`) del intercambio en formato `YYYYMMDD` / `HHMMSS`.
- **Estados de recepción (ETAREC):** `00` En entrada, `10` Pendiente planificar, `20` Pendiente recepción, `30` Recepción en curso, `35` Distribución en curso, `40` Recibido, `50` Enviado, `90` Cancelado, `95` Archivado.
- **Estados de expedición (ETALIV):** `00` En entrada, `10` Pendiente ola, `20` Seleccionado en ola, `30` A preparar, `35` En preparación, `40` Validado, `50` Enviado, `60` Expedido, `90` Cancelado, `95` Archivado.
- **Bloqueo de orden:** Los indicadores `BLOREC` y `BLOLIV` señalan si la orden está bloqueada en el WMS en el momento de la notificación.
- **Información adicional de expedición:** El estado de una orden de expedición puede incluir número de ola (`NUMVAG`), muelle de carga (`KAILIV`), indicador de ruptura total (`RUPTOT`) y cancelación de ola (`ANLVAG`).

> **Nota importante:** Cada mensaje a través del nodo principal (`status`) contiene exclusivamente registros de recepción (`statusReceptionOrders`) **o** de expedición (`statusDeliveryOrders`), nunca ambos a la vez. El ERP debe gestionar ambos arrays de forma independiente.

### Integración

Este mensaje es enviado automáticamente por el WMS cada vez que cambia el estado de una orden.
El ERP debe mantener un endpoint activo y accesible para recibir las notificaciones y actualizar su propio estado de seguimiento.
Las referencias `REFREC` y `REFLIV` corresponden a las mismas referencias declaradas en los mensajes **GECOM40** y **GECOM50** respectivamente.