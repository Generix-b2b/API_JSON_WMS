## GECOM20 — Customer Master Data

Mensaje para la declaración y mantenimiento del **maestro de clientes** en el WMS Generix Spain.
Permite crear, modificar o cancelar registros de cliente de forma sincronizada entre el ERP y el WMS.

### Características Principales

- **Operaciones soportadas (TRTEXC):** Creación (`1`), modificación o creación (`2`) y cancelación (`9`). El valor por defecto es `2`.
- **Identificación única:** El campo `CODCLI` es la clave del cliente en el WMS. Debe coincidir con el código maestro del sistema origen (ERP).
- **Tipo de cliente (TYPCLI):** Punto de entrega final (`1`), cliente agrupador (`2`), plataforma (`3`) o taller (`4`).
- **Dirección completa:** Hasta 3 líneas de dirección (`AD1CLI`, `AD2CLI`, `AD3CLI`) más ciudad, código postal y país en formato ISO 3166 alpha-2 o alpha-3.
- **Bloque adicional (GEEX2001):** Datos de contacto, transportista, rondas de entrega (hasta 7), gestión de alcohol, control de calidad, comentarios (hasta 3 líneas) y nombres adicionales del cliente.
- **Rubriques del cliente (GEEX2050):** Array de hasta 99 etiquetas de clasificación con código de sección (`CODRUB`) y valor (`VALRUB`), en codificación interna o estándar EDIFACT.

> **Nota importante:** Cuando `TRTEXC = 2` el mensaje reemplaza la ficha completa del cliente, incluyendo los bloques `GEEX2001` y `GEEX2050`.

### Integración

Este mensaje debe enviarse al WMS **antes** de procesar órdenes de expedición del cliente.
La sincronización es necesaria para que el cliente esté registrado como destino válido en el almacén.
Un cliente no declarado generará un error de rechazo en los mensajes de salida de mercancía.
