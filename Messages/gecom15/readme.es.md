## GECOM15 — Carrier Master Data

Mensaje para la declaración y mantenimiento del **maestro de transportistas** en el WMS Generix Spain.
Permite crear, modificar o cancelar registros de transportistas de forma sincronizada entre el ERP y el WMS.

### Características Principales

- **Operaciones soportadas (TRTEXC):** Creación (`1`), modificación o creación (`2`) y cancelación (`9`). El valor por defecto es `2`.
- **Identificación única:** El campo `CODTRA` es la clave del transportistas en el WMS. Debe coincidir con el código maestro del sistema origen (ERP).
- **Dirección completa:** Hasta 3 líneas de dirección (`AD1TRA`, `AD2TRA`, `AD3TRA`) más ciudad, código postal y país.
- **Bloque adicional (GEEX1501):** Datos de contacto, email, incoterms, control de calidad, gestión de series, comentarios libres (hasta 3 líneas) y nombres adicionales del transportistas.

> **Nota importante:** Cuando `TRTEXC = 2` el mensaje reemplaza la ficha completa del transportistas, incluyendo el bloque `GEEX1501`.
>!green El campo **RCTEXC** es muy importante que este correctamente cumplimentado, para poder redirigir los mensajes a la librería de WMS correcta. La información de este valor es diferente para test y producción, el dato podrá ser proporcionado por el consultor WMS.

### Integración

Este mensaje debe enviarse al WMS **antes** de procesar órdenes de recepción del proveedores.
La sincronización es necesaria para que el transportistas esté registrado como origen válido en el almacén.
Un transportistas no declarado generará un error de rechazo en los mensajes de entrada de mercancía.