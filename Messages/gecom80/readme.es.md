## GECOM80 — Stock Movement

Mensaje de **notificación de movimientos de stock** enviado por el WMS Generix Spain al sistema origen (ERP).
Informa de cada movimiento físico o administrativo que afecta al inventario del almacén, permitiendo al ERP mantener su stock sincronizado en tiempo real.

### Características Principales

- **Dirección del flujo:** Outbound — el WMS publica este mensaje en el endpoint del cliente (`POST https://[URL_Client]/endpoint`) cada vez que se produce un movimiento.
- **Tipo de movimiento (CODMVT):** Administrativo (`00`), entrada/almacenamiento (`10`), salida/destocking (`20`), transferencia (`30`), ajuste de cantidad (`40`) o inmovilización (`80`).
- **Sentido del movimiento (SENMVT):** `+` para almacenamiento o desinmovilización, `-` para salida o inmovilización.
- **Identificación de la mercancía:** Producto (`CODPRO`), variante logística, lote (`CODLOT`), palé EAN128 (`CODPAL`) y ubicación completa (zona, pasillo, columna, nivel).
- **Tercero y pedido asociado:** Código de tercero (`CODTIE`) con su tipo (proveedor/cliente) y número de orden de recepción o entrega (`NUMCDE`) que originó el movimiento.
- **Información adicional (GEEX8001):** Datos de análisis, pesos, códigos SAP (motivo, ubicación, estado) y familia de producto.
- **Inmovilización (GEEX8060):** Bloque para movimientos de inmovilización/desinmovilización, con fechas, horas y motivos.
- **Liberación positiva (GEEX8090):** Bloque para movimientos complementarios de liberación de palés, con estado del palé (`ETAPAL`) y gestión de listas negras (black list).

> **Nota importante:** Este mensaje es generado por el WMS; el código de proceso `TRTEXC` viene siempre vacío. Los campos obligatorios mínimos son la actividad (`CODACT`), el producto (`CODPRO`) y el tipo de movimiento (`CODMVT`).
>!green El campo **RCTEXC** es muy importante que este correctamente cumplimentado, para poder redirigir los mensajes a la librería de WMS correcta. La información de este valor es diferente para test y producción, el dato podrá ser proporcionado por el consultor WMS.

### Integración

El ERP debe mantener un endpoint activo para recibir las notificaciones de movimiento y actualizar su contabilidad de stock.
Este mensaje proporciona la traza detallada de cada operación; para una foto completa del inventario en un instante dado, utilice **GECOM90**.