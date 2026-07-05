## GECOM08 — Table Load

Mensaje para la carga y mantenimiento de **tablas paramétricas** en el WMS Generix Spain.
Permite declarar los valores de configuración (familias de parámetros y sus claves) que son referenciados por el resto de mensajes del interfaz.

### Características Principales

- **Operaciones soportadas (TRTEXC):** Creación (`1`), modificación o creación (`2`) y cancelación (`9`). El valor por defecto es `2`.
- **Identificación del parámetro:** La combinación de familia (`FAMPAR`, hasta 3 caracteres) y clave (`CLEPAR`, hasta 10 caracteres) identifica de forma única cada entrada en la tabla.
- **Etiquetas:** Cada entrada admite una etiqueta principal (`LIBPAR`, hasta 48 caracteres) y opcionalmente una segunda etiqueta (`LIBPAR2`) y una segunda clave (`CLEPAR2`) para estructuras de parámetro doble.
- **Capacidad:** Hasta 499 registros por mensaje, sin bloques adicionales ni arrays anidados.

> **Nota importante:** Las familias de parámetros (`FAMPAR`) deben estar acordadas con el equipo de implantación de Generix. Una clave no declarada en las tablas generará errores de validación en los mensajes que la referencien.
>!blue El campo **RCTEXC** es muy importante que este correctamente cumplimentado, para poder redirigir los mensajes a la librería de WMS correcta. La información de este valor es diferente para test y producción, el dato podrá ser proporcionado por el consultor WMS.

### Integración

Este mensaje debe enviarse al WMS **antes** que cualquier otro mensaje del interfaz, ya que los códigos declarados aquí son utilizados como valores válidos en campos como `CODTRE`, `CODTLI`, `CODMOP` o `ABCPRO`, entre otros.
Una tabla incompleta o incorrecta puede provocar rechazos en cadena en los mensajes de maestros y transaccionales.
