## GECOM41 — Reception Order Confirmation

Mensaje de **notificación de recepción de órdenes** enviado por el WMS Generix Spain al sistema origen (ERP). Informa del cierre de la recepción y de la mercancía efectivamente recibida por el almacén para el pedido en cuestión.

### Características Principales

- **Dirección del flujo:** Outbound — el WMS publica este mensaje en el endpoint del cliente (`POST https://[URL_Client]/endpoint`). El ERP debe exponerlo y procesarlo.
- **Identificación:** La referencia `REFREC`, junto con el número de orden (`NUMREC`) y el proveedor (`CODFOU`), enlaza la confirmación con la orden original. El origen del pedido se indica en `ORICDE` (interfaz, entrada local, reintegración global o recepción a verificar).
- **Fechas de seguimiento:** Distingue entre fecha prevista (`DTIREC`), reprogramada (`DTMREC`) y real de recepción (`DTRREC`), permitiendo al ERP medir desviaciones.
- **Información adicional de cabecera (GEEX4101):** Datos de albarán, temperatura del camión, información veterinaria y aduanera, y motivos de recepción o rechazo.
- **Líneas recibidas (GEEX4120):** Array de hasta 999 líneas con el desglose por producto: cantidad pedida (`UVCREA`), recibida (`UVCREC`), gratuita (`UVCGRA`), inmovilizada (`UVCIMM`), rechazada (`UVCRFU`) y en reliquat/backorder (`UVCRLQ`), con sus motivos asociados.
- **Detalle por soporte (GEEX4130):** Anidado en cada línea, identifica lote, palé (EAN128), ubicación de almacenamiento y números de serie (`GEEX4140`).
- **Embalajes recibidos (GEEX4180):** Array de hasta 99 entradas para la gestión de embalajes retornables (entrada/salida).
- **Totales (GEEX4199):** Resumen con número de líneas, soportes, bultos y productos de la orden.

> **Nota importante:** Este mensaje es generado por el WMS; el código de proceso `TRTEXC` solo admite vacío o `2` (modificación). El ERP debe usar la referencia `REFREC` para conciliar la confirmación con la orden **GECOM40** correspondiente.
>!blue El campo **RCTEXC** es muy importante que este correctamente cumplimentado, para poder redirigir los mensajes a la librería de WMS correcta. La información de este valor es diferente para test y producción, el dato podrá ser proporcionado por el consultor WMS.

### Integración

Este mensaje es enviado automáticamente por el WMS cuando se cierra la recepción del pedido por parte del almacén. El ERP debe mantener un endpoint activo y accesible para recibir las notificaciones y actualizar la información del pedido. Las referencias `REFREC`, `CODACT`, `CODTRE`, `NLIREC`, `CODPRO`, etc. corresponden a las mismas referencias declaradas en el mensaje **GECOM40**.
