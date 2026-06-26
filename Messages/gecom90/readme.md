## GECOM90 — Stock Photo

Mensaje de **foto de stock (snapshot de inventario)** enviado por el WMS Generix Spain al sistema origen (ERP).
Proporciona una imagen completa del inventario del almacén en un instante dado, agregada según distintos criterios de consulta.

### Características Principales

- **Dirección del flujo:** Outbound — el WMS publica este mensaje en el endpoint del cliente (`POST https://[URL_Client]/endpoint`), normalmente de forma programada o bajo demanda.
- **Niveles de agregación disponibles:** Cada mensaje contiene **uno solo** de los siguientes seis desgloses (ver Nota importante).
- **Por producto y lote (GEEX9000):** Totales de CSU, bultos y palés con desglose por estado (en curso, reservado, inmovilizado, comercializable) y fechas extremas de recepción y caducidad.
- **Por producto / caducidad / inmovilización (GEEX9008):** Stock agrupado por `CODPRO`, fecha de caducidad y motivo de inmovilización, con signo de cantidad y peso.
- **Por producto / inmovilización (GEEX9009):** Stock agrupado por `CODPRO` y motivo de inmovilización.
- **Por producto / ubicación (GEEX9020):** Detalle por ubicación física con número de foto, tipo (stock, durmiente, ubicación) e indicadores de ocupación.
- **Por número de serie (GEEX9040):** Trazabilidad unitaria con estado del número de serie (recibido, preparado, expedido) y referencias de pedido asociadas.
- **Por SSCC (GEEX9070):** Detalle a nivel de palé/soporte EAN128 con estado, inmovilización, ubicación y movimiento.

> **Nota importante:** Cada mensaje contiene exclusivamente uno de los seis tipos de desglose (regla `oneOf`), nunca varios a la vez. El código de proceso `TRTEXC` viene vacío salvo en el desglose por SSCC, que admite además simulación (`8`). Cada array soporta hasta 9.999 registros.

### Integración

El ERP debe mantener un endpoint activo para recibir la foto de stock y conciliar su inventario con el del WMS.
A diferencia de **GECOM80** (que notifica movimientos individuales), este mensaje ofrece el estado consolidado del stock en un momento concreto, ideal para conciliaciones periódicas e inventarios.
