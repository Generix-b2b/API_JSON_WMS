## GECOM10 — Supplier Master Data

Message for declaring and maintaining the **supplier master** in the Generix Spain WMS.
It allows creating, modifying or cancelling supplier records in a synchronized way between the ERP and the WMS.

### Key Features

- **Supported operations (TRTEXC):** Create (`1`), modify or create (`2`) and cancellation (`9`). The default value is `2`.
- **Unique identification:** The `CODFOU` field is the supplier key in the WMS. It must match the master code of the source system (ERP).
- **Full address:** Up to 3 address lines (`AD1FOU`, `AD2FOU`, `AD3FOU`) plus city, postal code and country.
- **Additional block (GEEX1001):** Contact details, email, incoterms, quality control, serial-number management, free comments (up to 3 lines) and additional supplier names.
- **Reception management:** Configures the behavior of shipping notices (`GSTAVI`), RF management (`GSTRCP`) and connector type (`TYPPRT`).

> **Important note:** When `TRTEXC = 2`, the message replaces the supplier's entire record, including the `GEEX1001` block.

### Integration

This message must be sent to the WMS **before** processing supplier reception orders.
Synchronization is required so that the supplier is registered as a valid source in the warehouse.
An undeclared supplier will generate a rejection error in the goods-receipt messages.