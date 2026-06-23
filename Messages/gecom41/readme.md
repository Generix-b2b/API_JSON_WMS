## GECOM41 — Reception Order Confirmation

Mensaje de **notificación de recepción de órdenes** enviado por el WMS Generix Spain al sistema origen (ERP).
Informa en del cierre de la recepción y la mercancía recibida por el almacén del pedido en cuestión.

### Características Principales

- **Dirección del flujo:** Outbound — el WMS publica este mensaje en el endpoint del cliente (`POST https://[URL_Client]/endpoint`). El ERP debe exponerlo y procesarlo.


> **Nota importante:** Cada mensaje a través del nodo principial (`status`) contiene exclusivamente registros de recepción (`statusReceptionOrders`) **o** de expedición (`statusDeliveryOrders`), nunca ambos a la vez. El ERP debe gestionar ambos arrays de forma independiente.

### Integración

Este mensaje es enviado automáticamente por el WMS cuando se cierra la recepción del pedido por parte del almacén.
El ERP debe mantener un endpoint activo y accesible para recibir las notificaciones y actualizar la información del pedido.
Las referencia `REFREC`,`CODACT`,`CODTRE`,`NLIREC`,`CODPRO`, etc.. corresponde a las mismas referencias declaradas en el mensaje **GECOM40**.
