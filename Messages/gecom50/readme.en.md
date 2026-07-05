## GECOM50 — Delivery Orders

Message for creating and maintaining **delivery orders** in the Generix Spain WMS.
It allows creating, modifying or cancelling goods-issue orders in a synchronized way between the ERP and the WMS.

### Key Features

- **Supported operations (TRTEXC):** Create (`1`), modify or create (`2`), header modification (`7`) and cancellation (`9`). The default value is `2`.
- **Order identification:** The `REFLIV` reference identifies the order in the WMS. The `NUMLIV` and `SNULIV` fields allow referencing the number and sub-number of the source order. The header includes delivery type (`CODTLI`), expected date and time (`DTILIV`, `HEILIV`), carrier (`CODTRA`), shipping round and dock (`TOULIV`, `KAILIV`) and messages printable on the picking sheet and the delivery note (`MSGPRP`, `MSGLIV`, up to 2 lines each).
- **Order type (TYPCDE):** Distinguishes between a firm order (`false`) and a provisional one (`true`). Provisional orders do not generate picking until they are confirmed.
- **Alcohol management (GSTALC):** Configurable at header level: no management (`0`), delivery with DSAC (`1`), delivery with DAC (`2`) or tax-exempt (`3`).
- **Additional header information (GEEX5001):** Dispatch and loading dates, the recipient's order reference, GLN code, intermediate relay point (`CLIVIA`), cancellation code and route number.
- **VPC delivery address (GEEX5010):** Optional block with the name and full address of the final recipient. It allows overriding the master data for e-commerce deliveries or orders with an ad hoc address.
- **Order lines (GEEX5020):** Array of up to 99 lines, each with product (`CODPRO`), quantity in CSU (`UVCCDE`), batch, product substitution, operation type (promotion/reservation) and price marking. Required when `TRTEXC = 1` or `2`.
- **Headings:** At header level (`GEEX5005`) and line level (`GEEX5025`), up to 99 traceability attributes per level. Line headings also accept minimum and maximum value ranges for batch control.
- **Free text (GEEX5080):** Array of up to 99 free-text lines printed on the delivery note (up to 120 characters per line).

> **Important note:** When `TRTEXC = 2`, the message replaces the order's entire record, including all its lines. To modify only the header without affecting the existing lines, use `TRTEXC = 7`.
>!green The **RCTEXC** field must be correctly populated, as it is essential for routing messages to the appropriate WMS library. The value for this field differs between the test and production environments. The correct value can be provided by the WMS consultant.

### Integration

This message must be sent to the WMS **before** the start of the order picking process.
The customer referenced in `CODCLI` must be previously declared via **GECOM20**.
An undeclared order will prevent the generation of picking work and will generate a rejection error in the shipping process.