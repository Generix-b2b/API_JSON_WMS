## GECOM97 — Status Orders

**Status notification** message for reception and delivery orders, sent by the Generix Spain WMS to the source system (ERP).
It reports in real time the status changes that occur in the warehouse during an order's life cycle.

### Key Features

- **Flow direction:** Outbound — the WMS publishes this message to the client endpoint (`POST https://[URL_Client]/endpoint`). The ERP must expose and process it.
- **Supported operations (TRTEXC):** Modify or create (`2`). The default value is `2`.
- **Exchange metadata:** Each record includes sender (`EMTEXC`), receiver (`RCTEXC`), date (`DATEXC`) and time (`HEUEXC`) of the exchange in `YYYYMMDD` / `HHMMSS` format.
- **Reception statuses (ETAREC):** `00` Incoming, `10` Pending planning, `20` Pending reception, `30` Reception in progress, `35` Distribution in progress, `40` Received, `50` Sent, `90` Cancelled, `95` Archived.
- **Delivery statuses (ETALIV):** `00` Incoming, `10` Pending wave, `20` Selected in wave, `30` To prepare, `35` In preparation, `40` Validated, `50` Sent, `60` Dispatched, `90` Cancelled, `95` Archived.
- **Order block:** The `BLOREC` and `BLOLIV` indicators signal whether the order is blocked in the WMS at the time of the notification.
- **Additional delivery information:** The status of a delivery order may include wave number (`NUMVAG`), loading dock (`KAILIV`), total shortage indicator (`RUPTOT`) and wave cancellation (`ANLVAG`).

> **Important note:** Each message, through the main node (`status`), contains exclusively reception records (`statusReceptionOrders`) **or** delivery records (`statusDeliveryOrders`), never both at once. The ERP must handle both arrays independently.
>!blue The **RCTEXC** field must be correctly populated, as it is essential for routing messages to the appropriate WMS library. The value for this field differs between the test and production environments. The correct value can be provided by the WMS consultant.

### Integration

This message is sent automatically by the WMS each time an order's status changes.
The ERP must keep an active and accessible endpoint to receive the notifications and update its own tracking status.
The references `REFREC` and `REFLIV` correspond to the same references declared in the **GECOM40** and **GECOM50** messages respectively.