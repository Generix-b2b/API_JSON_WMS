## GECOM30 (EAN) — Product Master Data (EAN)

Message for declaring and maintaining the **product EAN/EDI codes** in the Generix Spain WMS.
It complements the **GECOM30** product master by allowing the multiple barcodes associated with each item to be declared independently.

### Key Features

- **Flow direction:** Inbound — the ERP sends this message to the WMS (`POST https://[URL_Client_Environment].generix.biz/m30_ean?uuid=[Value]`).
- **Supported operations (TRTEXC):** Create (`1`), modify or create (`2`) and cancellation (`9`). The default value is `2`.
- **Product identification:** The combination of activity (`CODACT`), product (`CODPRO`) and logistics variant (`VALPRO`) links the EAN code with its item in the master.
- **EDI code (EDIPRO):** This is the barcode itself, with its associated designation (`EANDS1`).
- **Main or secondary code (EDIPRM):** Distinguishes the primary code (`true`) from the secondary one (`false`). Each product must have a single primary code per level.
- **Level qualifier (EDIQLF):** Indicates which logistics unit the code corresponds to: CSU (`0`), multi-product batch (`1`), SPCB (`2`), PCB (`3`), case (`4`) or pallet (`5`).
- **Sales EAN (EANVTE):** Marks whether the code is suitable for sale (`true`) or not (`false`).

> **Important note:** This message decouples EAN code management from the main product master. The product referenced in `CODPRO` must already exist, declared via **GECOM30**. The required fields are `TRTEXC`, `CODACT`, `CODPRO`, `EDIPRO`, `EDIPRM` and `EDIQLF`.
>!blue The **RCTEXC** field must be correctly populated, as it is essential for routing messages to the appropriate WMS library. The value for this field differs between the test and production environments. The correct value can be provided by the WMS consultant.

### Integration

This message must be sent to the WMS **after** declaring the product in the **GECOM30** master and **before** processing movements that reference its barcodes.
It allows adding, modifying or removing EAN codes without needing to resend the product's full record, which is especially useful for items with multiple packaging levels.