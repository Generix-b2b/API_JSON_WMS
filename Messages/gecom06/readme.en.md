### GECOM06 - Pallet Blocking/Unblocking Request

Message used to request the blocking or unblocking of **pallets** in Generix Spain WMS.
It allows blocking or unblocking records for goods to be created, updated, or cancelled between the ERP and the WMS.

#### Main Features
- **Supported operations (TRTEXC):** Creation (`1`), modification or creation (`2`), and cancellation (`9`). The default value is 2.
- **Parameter identification:** The combination of `CODPAL`, `CODACT`, `CODTRT` and `MOTIMM` uniquely identifies the blocking/unblocking of the goods.
- **Capacity:** Up to 499 records per message, with no additional blocks or nested arrays.

**Important note:** Reasons for blocking or unblocking (`MOTIMM`) must be agreed with the Generix implementation team. A reason code that is not declared in the tables will generate validation errors in the messages that reference it.

!green The **RCTEXC** field is very important and must be correctly filled in so that messages can be routed to the correct WMS library. This value is different for test and production environments, and it may be provided by the WMS consultant.

#### Integration

This message must be sent to the WMS **after** the physical arrival of the goods at the warehouse.
