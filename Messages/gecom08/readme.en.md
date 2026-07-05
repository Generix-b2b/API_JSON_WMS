## GECOM08 — Table Load

Message for loading and maintaining **parameter tables** in the Generix Spain WMS.
It declares the configuration values (parameter families and their keys) that are referenced by the rest of the interface messages.

### Key Features

- **Supported operations (TRTEXC):** Create (`1`), modify or create (`2`) and cancellation (`9`). The default value is `2`.
- **Parameter identification:** The combination of family (`FAMPAR`, up to 3 characters) and key (`CLEPAR`, up to 10 characters) uniquely identifies each entry in the table.
- **Labels:** Each entry accepts a main label (`LIBPAR`, up to 48 characters) and, optionally, a second label (`LIBPAR2`) and a second key (`CLEPAR2`) for double-parameter structures.
- **Capacity:** Up to 499 records per message, with no additional blocks or nested arrays.

> **Important note:** Parameter families (`FAMPAR`) must be agreed with the Generix implementation team. A key that is not declared in the tables will generate validation errors in the messages that reference it.
>!green The **RCTEXC** field must be correctly populated, as it is essential for routing messages to the appropriate WMS library. The value for this field differs between the test and production environments. The correct value can be provided by the WMS consultant.

### Integration

This message must be sent to the WMS **before** any other interface message, since the codes declared here are used as valid values in fields such as `CODTRE`, `CODTLI`, `CODMOP` or `ABCPRO`, among others.
An incomplete or incorrect table can cause cascading rejections in the master-data and transactional messages.
