## GECOM10 — Carrier Master Data

Message for declaring and maintaining the **carrier master** in the Generix Spain WMS.
It allows creating, modifying or cancelling carrier records in a synchronized way between the ERP and the WMS.

### Key Features

- **Supported operations (TRTEXC):** Create (`1`), modify or create (`2`) and cancellation (`9`). The default value is `2`.
- **Unique identification:** The `CODTRA` field is the carrier key in the WMS. It must match the master code of the source system (ERP).
- **Full address:** Up to 3 address lines (`AD1TRA`, `AD2TRA`, `AD3TRA`) plus city, postal code and country.
- **Additional block (GEEX1501):** Contact details, email, incoterms, quality control, serial-number management, free comments (up to 3 lines) and additional carrier names.

> **Important note:** When `TRTEXC = 2`, the message replaces the carrier's entire record, including the `GEEX1501` block.
>!green The **RCTEXC** field must be correctly populated, as it is essential for routing messages to the appropriate WMS library. The value for this field differs between the test and production environments. The correct value can be provided by the WMS consultant.

### Integration

This message must be sent to the WMS **before** processing supplier reception orders.
Synchronization is required so that the carrier is registered as a valid source in the warehouse.
An undeclared carrier will generate a rejection error in the goods-receipt messages.