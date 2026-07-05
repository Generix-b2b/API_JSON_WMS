## GECOM40 — Reception Orders

Message for creating and maintaining **reception orders** in the Generix Spain WMS.
It allows creating, modifying or cancelling goods-receipt orders in a synchronized way between the ERP and the WMS.

### Key Features

- **Supported operations (TRTEXC):** Create (`1`), modify or create (`2`), header modification (`7`) and cancellation (`9`). The default value is `2`.
- **Order identification:** The `REFREC` reference identifies the order in the WMS. The `NUMREC` and `SNUREC` fields allow referencing the number and sub-number of the source order.
- **Header:** Includes supplier (`CODFOU`), reception type (`CODTRE`), expected date and time (`DTIREC`, `HEIREC`), reception dock (`KAIREC`), transport method (`METTRP`) and a message printable on the delivery note (`MSGREC`, up to 2 lines).
- **Supplier information (GEEX4001):** Optional block with name, full address and supplier type. It allows overriding the master data for this specific reception.
- **Order lines (GEEX4020):** Array of up to 99 lines, each with product (`CODPRO`), quantity in CSU (`UVCREA`), batch, manufacturing dates and palletization dimensions. Required when `TRTEXC = 1` or `2`.
- **Serial numbers per line (GEEX4040):** Array nested in each line with up to 99 serial numbers, identifying the type (CSU or case) and the EAN128 pallet code.
- **Headings:** At header level (`GEEX4005`) and line level (`GEEX4025`), up to 99 traceability labels per level.
- **Free text (GEEX4080):** Array of up to 99 free-text lines associated with the order (up to 120 characters per line).

> **Important note:** When `TRTEXC = 2`, the message replaces the order's entire record, including all its lines. To modify only the header without affecting the existing lines, use `TRTEXC = 7`.
>!green The **RCTEXC** field must be correctly populated, as it is essential for routing messages to the appropriate WMS library. The value for this field differs between the test and production environments. The correct value can be provided by the WMS consultant.

### Integration

This message must be sent to the WMS **before** the physical arrival of the goods at the warehouse.
The supplier referenced in `CODFOU` must be previously declared via **GECOM10**.
An undeclared order will prevent the reception from being recorded and will generate a rejection error in the inbound process.