## GECOM49 — Dispatch Advice

Message for declaring **dispatch advices (DESADV)** in the Generix Spain WMS.
It allows notifying the warehouse of the exact content of a shipment before its physical arrival, making reception planning easier.

### Key Features

- **Supported operations (TRTEXC):** Create (`1`), modify (`2`) and cancellation (`9`). The default value is `2`.
- **Advice identification:** The `AVIREF` field is the unique reference of the DESADV in the WMS. The header also includes dispatch date and time (`DATEXP`, `HEUEXP`), expected delivery date and time (`DATLIV`, `HEULIV`), delivery note number (`REFLET`), truck number (`CAMCOD`) and seal (`REFPLB`).
- **Automatic reception creation:** The `CRERCP = true` indicator instructs the WMS to automatically generate a reception order from this advice, without needing to send a separate **GECOM40** message.
- **Partial shipment control (INDSBY):** Allows sending the advice in held mode (`1`) to complete it with successive messages, and releasing it with the last shipment (`2`).
- **Logistics objects (GEEX4910):** Array of up to 99 pallets or packages, each identified by its code (`CODOBL`) and line number (`AVINLI`). It includes weight, dimensions, marking type and packaging codes. Required when `TRTEXC = 1` or `2`.
- **Logistics object detail:** Each logistics object contains nested sub-blocks with the product and batch (`GEEX4920`, required), manufacturing data and reception reference (`GEEX4921`), delivery reference and price (`GEEX4922`), and promotion or immobilization data (`GEEX4923`).
- **Headings:** At header level (`GEEX4905`) and logistics-object level (`GEEX4925`), up to 99 traceability attributes per level.

> **Important note:** Unlike **GECOM40**, the GECOM49 model organizes goods by logistics objects (pallets, packages), not by product lines. The product and quantity are declared within the `GEEX4920` sub-block of each object.
>!green The **RCTEXC** field must be correctly populated, as it is essential for routing messages to the appropriate WMS library. The value for this field differs between the test and production environments. The correct value can be provided by the WMS consultant.

### Integration

This message must be sent to the WMS **before** the physical arrival of the truck at the warehouse.
The supplier referenced in `CODFOU` must be previously declared via **GECOM10**.
If `CRERCP = false`, the corresponding reception order must exist in the WMS (declared via **GECOM40**) so that the advice can be correctly associated.