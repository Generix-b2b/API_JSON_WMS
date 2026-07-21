## GECOM06 — Solicitud de bloqueo/desbloqueo de palés

Mensaje para la solicitud de Bloqueo o Desbloqueo de **Palés** en el WMS Generix Spain.
Permite crear, modificar o cancelar registros de bloqueo o desbloqueo de mercancía entre el ERP y el WMS.

### Características Principales

- **Operaciones soportadas (TRTEXC):** Creación (`1`), modificación o creación (`2`) y cancelación (`9`). El valor por defecto es `2`.
- **Identificación del parámetro:** La combinación de `CODPAL`, `CODACT`, `CODPRO` y `MOTIMM` identifica de forma única el bloqueo / desbloqueo de la mercancía.
- **Capacidad:** Hasta 499 registros por mensaje, sin bloques adicionales ni arrays anidados.

> **Nota importante:** Las familias de parámetros (`MOTIMM`) deben estar acordadas con el equipo de implantación de Generix. Una motivo no declarado en las tablas generará errores de validación en los mensajes que la referencien.
>!green El campo **RCTEXC** es muy importante que este correctamente cumplimentado, para poder redirigir los mensajes a la librería de WMS correcta. La información de este valor es diferente para test y producción, el dato podrá ser proporcionado por el consultor WMS.

### Integración

Este mensaje debe enviarse al WMS **después** de la llegada física de la mercancía al almacén.
