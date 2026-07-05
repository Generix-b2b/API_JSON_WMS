## GECOM10 — Supplier Master Data

Mensaje para la declaración y mantenimiento del **maestro de proveedores** en el WMS Generix Spain.
Permite crear, modificar o cancelar registros de proveedor de forma sincronizada entre el ERP y el WMS.

### Características Principales

- **Operaciones soportadas (TRTEXC):** Creación (`1`), modificación o creación (`2`) y cancelación (`9`). El valor por defecto es `2`.
- **Identificación única:** El campo `CODFOU` es la clave del proveedor en el WMS. Debe coincidir con el código maestro del sistema origen (ERP).
- **Dirección completa:** Hasta 3 líneas de dirección (`AD1FOU`, `AD2FOU`, `AD3FOU`) más ciudad, código postal y país.
- **Bloque adicional (GEEX1001):** Datos de contacto, email, incoterms, control de calidad, gestión de series, comentarios libres (hasta 3 líneas) y nombres adicionales del proveedor.
- **Gestión de recepción:** Configura el comportamiento de avisos de envío (`GSTAVI`), gestión RF (`GSTRCP`) y tipo de conector (`TYPPRT`).

> **Nota importante:** Cuando `TRTEXC = 2` el mensaje reemplaza la ficha completa del proveedor, incluyendo el bloque `GEEX1001`.
>!green El campo **RCTEXC** es muy importante que este correctamente cumplimentado, para poder redirigir los mensajes a la librería de WMS correcta. La información de este valor es diferente para test y producción, el dato podrá ser proporcionado por el consultor WMS.

### Integración

Este mensaje debe enviarse al WMS **antes** de procesar órdenes de recepción del proveedor.
La sincronización es necesaria para que el proveedor esté registrado como origen válido en el almacén.
Un proveedor no declarado generará un error de rechazo en los mensajes de entrada de mercancía.