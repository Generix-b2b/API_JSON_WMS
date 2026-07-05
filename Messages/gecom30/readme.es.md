## GECOM30 — Product Master Data

Mensaje para la declaración y mantenimiento del **maestro de productos** en el WMS Generix Spain.
Permite crear, modificar o cancelar fichas de producto de forma sincronizada entre el ERP y el WMS.

### Características Principales

- **Operaciones soportadas (TRTEXC):** Creación (`1`), modificación o creación (`2`) y cancelación (`9`). El valor por defecto es `2`.
- **Identificación única:** El campo `CODPRO` es la clave del producto en el WMS, complementado por la variante logística `VALPRO`. Deben coincidir con el código maestro del sistema origen (ERP).
- **Dimensiones físicas:** Pesos y medidas (altura, longitud, anchura) a nivel de CSU, caja (`COL`) y SPCB, más configuración de paletización (cajas por capa, capas por palet).
- **Gestión de almacenamiento:** Clase ABC, método de almacenamiento, zona y pasillo preferidos, homogeneidad de gaveta y modo de recepción (`MODREC`).
- **Bloques adicionales (GEEX3001–GEEX3004):** Datos de marca, circuitos de preparación, sustitución de producto, gestión de alcohol (grado, volumen, sello), mercancías peligrosas, temperaturas, trazabilidad, inmobilización, datos multimateria y códigos de impuestos especiales.
- **Códigos EAN (GEEX3020):** Array de hasta 49 códigos EDI con su cualificador de nivel (CSU, SPCB, caja, palet…) e indicador de código principal.
- **Componentes BOM (GEEX3010):** Array de hasta 99 componentes para productos compuestos (`TOPPRN = 1`), con cantidad requerida y tipo (principal/secundario).
- **Bloques de clasificación y extensión:** Designaciones multiidioma (`GEEX3030`), declaraciones ICPE (`GEEX3040`), rubriques (`GEEX3050`), datos satélite (`GEEX3060`) y productos sustitutos (`GEEX3080`), todos con capacidad de hasta 99 entradas.

> **Nota importante:** Cuando `TRTEXC = 2` el mensaje reemplaza la ficha completa del producto, incluyendo todos los bloques adicionales y arrays declarados.
>!green El campo **RCTEXC** es muy importante que este correctamente cumplimentado, para poder redirigir los mensajes a la librería de WMS correcta. La información de este valor es diferente para test y producción, el dato podrá ser proporcionado por el consultor WMS.

### Integración

Este mensaje debe enviarse al WMS **antes** de procesar cualquier movimiento de stock que referencie el producto.
La sincronización es necesaria para que el artículo esté registrado con sus atributos logísticos correctos en el almacén.
Un producto no declarado generará un error de rechazo en los mensajes de recepción, expedición e inventario.