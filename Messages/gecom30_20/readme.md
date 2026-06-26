## GECOM30 (EAN) — Product Master Data (EAN)

Mensaje para la declaración y mantenimiento de los **códigos EAN/EDI de producto** en el WMS Generix Spain.
Complementa el maestro de productos **GECOM30** permitiendo declarar de forma independiente los múltiples códigos de barras asociados a cada artículo.

### Características Principales

- **Dirección del flujo:** Inbound — el ERP envía este mensaje al WMS (`POST https://[URL_Client_Environment].generix.biz/m30_ean?uuid=[Value]`).
- **Operaciones soportadas (TRTEXC):** Creación (`1`), modificación o creación (`2`) y cancelación (`9`). El valor por defecto es `2`.
- **Identificación del producto:** La combinación de actividad (`CODACT`), producto (`CODPRO`) y variante logística (`VALPRO`) enlaza el código EAN con su artículo en el maestro.
- **Código EDI (EDIPRO):** Es el código de barras propiamente dicho, con su designación asociada (`EANDS1`).
- **Código principal o secundario (EDIPRM):** Distingue el código primario (`true`) del secundario (`false`). Cada producto debe tener un único código primario por nivel.
- **Cualificador de nivel (EDIQLF):** Indica a qué unidad logística corresponde el código: CSU (`0`), lote multiproducto (`1`), SPCB (`2`), PCB (`3`), caja (`4`) o palé (`5`).
- **EAN de venta (EANVTE):** Marca si el código es apto para venta (`true`) o no (`false`).

> **Nota importante:** Este mensaje desacopla la gestión de códigos EAN del maestro de producto principal. El producto referenciado en `CODPRO` debe existir previamente, declarado mediante **GECOM30**. Los campos obligatorios son `TRTEXC`, `CODACT`, `CODPRO`, `EDIPRO`, `EDIPRM` y `EDIQLF`.

### Integración

Este mensaje debe enviarse al WMS **después** de declarar el producto en el maestro **GECOM30** y **antes** de procesar movimientos que referencien sus códigos de barras.
Permite añadir, modificar o eliminar códigos EAN sin necesidad de reenviar la ficha completa del producto, lo que resulta especialmente útil para artículos con múltiples niveles de empaquetado.
