## GECOM30 — Product Master Data

Message for declaring and maintaining the **product master** in the Generix Spain WMS.
It allows creating, modifying or cancelling product records in a synchronized way between the ERP and the WMS.

### Key Features

- **Supported operations (TRTEXC):** Create (`1`), modify or create (`2`) and cancellation (`9`). The default value is `2`.
- **Unique identification:** The `CODPRO` field is the product key in the WMS, complemented by the logistics variant `VALPRO`. They must match the master code of the source system (ERP).
- **Physical dimensions:** Weights and measures (height, length, width) at CSU, case (`COL`) and SPCB level, plus palletization configuration (cases per layer, layers per pallet).
- **Storage management:** ABC class, storage method, preferred zone and aisle, tray homogeneity and reception mode (`MODREC`).
- **Additional blocks (GEEX3001–GEEX3004):** Brand data, preparation circuits, product substitution, alcohol management (degree, volume, seal), dangerous goods, temperatures, traceability, immobilization, multi-material data and excise tax codes.
- **EAN codes (GEEX3020):** Array of up to 49 EDI codes with their level qualifier (CSU, SPCB, case, pallet…) and main-code indicator.
- **BOM components (GEEX3010):** Array of up to 99 components for composite products (`TOPPRN = 1`), with required quantity and type (main/secondary).
- **Classification and extension blocks:** Multi-language designations (`GEEX3030`), ICPE declarations (`GEEX3040`), headings (`GEEX3050`), satellite data (`GEEX3060`) and substitute products (`GEEX3080`), all with a capacity of up to 99 entries.

> **Important note:** When `TRTEXC = 2`, the message replaces the product's entire record, including all declared additional blocks and arrays.
>!blue The **RCTEXC** field must be correctly populated, as it is essential for routing messages to the appropriate WMS library. The value for this field differs between the test and production environments. The correct value can be provided by the WMS consultant.

### Integration

This message must be sent to the WMS **before** processing any stock movement that references the product.
Synchronization is required so that the item is registered with its correct logistics attributes in the warehouse.
An undeclared product will generate a rejection error in the reception, shipping and inventory messages.