## GECOM90 — Stock Photo

**Stock photo (inventory snapshot)** message sent by the Generix Spain WMS to the source system (ERP).
It provides a complete image of the warehouse inventory at a given moment, aggregated according to different query criteria.

### Key Features

- **Flow direction:** Outbound — the WMS publishes this message to the client endpoint (`POST https://[URL_Client]/endpoint`), usually on a scheduled basis or on demand.
- **Available aggregation levels:** Each message contains **only one** of the following six breakdowns (see Important note).
- **By product and batch (GEEX9000):** Totals of CSU, packages and pallets broken down by status (in progress, reserved, immobilized, sellable) and earliest/latest reception and expiry dates.
- **By product / expiry / immobilization (GEEX9008):** Stock grouped by `CODPRO`, expiry date and immobilization reason, with quantity and weight sign.
- **By product / immobilization (GEEX9009):** Stock grouped by `CODPRO` and immobilization reason.
- **By product / location (GEEX9020):** Detail by physical location with photo number, type (stock, dormant, location) and occupancy indicators.
- **By serial number (GEEX9040):** Unit-level traceability with the serial number status (received, prepared, dispatched) and associated order references.
- **By SSCC (GEEX9070):** Detail at pallet/support level (EAN128) with status, immobilization, location and movement.

> **Important note:** Each message contains exclusively one of the six breakdown types (`oneOf` rule), never several at once. The process code `TRTEXC` comes empty except in the SSCC breakdown, which also accepts simulation (`8`). Each array supports up to 9,999 records.

### Integration

The ERP must keep an active endpoint to receive the stock photo and reconcile its inventory with that of the WMS.
Unlike **GECOM80** (which notifies individual movements), this message offers the consolidated state of the stock at a specific moment, ideal for periodic reconciliations and inventory counts.