## GECOM20 — Customer Master Data

Message for declaring and maintaining the **customer master** in the Generix Spain WMS.
It allows creating, modifying or cancelling customer records in a synchronized way between the ERP and the WMS.

### Key Features

- **Supported operations (TRTEXC):** Create (`1`), modify or create (`2`) and cancellation (`9`). The default value is `2`.
- **Unique identification:** The `CODCLI` field is the customer key in the WMS. It must match the master code of the source system (ERP).
- **Customer type (TYPCLI):** Final delivery point (`1`), grouping customer (`2`), platform (`3`) or workshop (`4`).
- **Full address:** Up to 3 address lines (`AD1CLI`, `AD2CLI`, `AD3CLI`) plus city, postal code and country.
- **Additional block (GEEX2001):** Contact details, carrier, delivery rounds (up to 7), alcohol management, quality control, comments (up to 3 lines) and additional customer names.
- **Customer headings (GEEX2050):** Array of up to 99 classification labels with section code (`CODRUB`) and value (`VALRUB`), in internal encoding or EDIFACT standard.

> **Important note:** When `TRTEXC = 2`, the message replaces the customer's entire record, including the `GEEX2001` and `GEEX2050` blocks.
>!green The **RCTEXC** field must be correctly populated, as it is essential for routing messages to the appropriate WMS library. The value for this field differs between the test and production environments. The correct value can be provided by the WMS consultant.

### Integration

This message must be sent to the WMS **before** processing customer shipping orders.
Synchronization is required so that the customer is registered as a valid destination in the warehouse.
An undeclared customer will generate a rejection error in the goods-issue messages.