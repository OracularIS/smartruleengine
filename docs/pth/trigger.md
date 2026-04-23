# Trigger Points


A trigger point is a specific moment in the system lifecycle where the Rule 
Engine can evaluate and execute rules.

When a business event occurs, an order is saved, a shipment is created, a 
trailer is dispatched, the system hits a trigger point. If the corresponding 
[hook](./hooks.md) is enabled, the Rule Engine evaluates any rules 
configured for that moment.

## Trigger Types

| Type | Description |
|---|---|
| **Before CRUD** | Fires before a record is written to the database. Used to validate or assign values pre-save |
| **At Created** | Fires after a record is successfully created. Full record data is available |
| **Event-based** | Fires when a specific system event occurs mid-workflow |


##  Trigger Points

A few trigger points are listed below.

### Order & Order Line

| Trigger Point | Type | Fires When |
|---|---|---|
| [`OSSI-ORD-BEFORE-CRUD`](./triggers/ossi-ord-before-crud.md) | Before CRUD | Before an order record is created or updated |
| [`OSSI-ORD_LINE-BEFORE-CRUD`](./triggers/ossi-ord-line-before-crud.md) | Before CRUD | Before an order line record is created or updated |
| [`OSSI-ORDER-CREATED`](./triggers/ossi-order-created.md) | At Created | After an order is successfully created |

### Shipment & Carrier

| Trigger Point | Type | Fires When |
|---|---|---|
| [`OSSI-SHIPMENT-CREATED`](./triggers/ossi-shipment-created.md) | At Created | After a shipment is created |
| [`OSSI-CARMOV-CREATED`](./triggers/ossi-carmov-created.md) | At Created | After a carrier movement record is created |
| [`OSSI-TRAILER-DISPATCHED`](./triggers/ossi-trailer-dispatched.md) | Event-based | When a trailer is dispatched |
| [`OSSI-CONSOLIDATE-SHIPMENT-LINES`](./triggers/ossi-consolidate-shipment-lines.md) | Event-based | During shipment line consolidation |

### Inventory & Work

| Trigger Point | Type | Fires When |
|---|---|---|
| [`OSSI-PICK-RELEASE`](./triggers/ossi-pick-release.md) | Event-based | During pick release and work execution |
| [`OSSI-INVENTORY-STATUS-CHANGE`](./triggers/ossi-inventory-status-change.md) | Event-based | When an inventory record status changes |

### Integration

| Trigger Point | Type | Fires When |
|---|---|---|
| [`OSSI-INTEGRATION`](./triggers/ossi-integration.md) | Event-based | During integration value mapping |

---
