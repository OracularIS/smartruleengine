# Hook Policy

## What is a Hook?

A hook is a gate that controls whether the Rule Engine responds to a system 
event. Even if rules are perfectly configured, nothing will execute unless the 
appropriate hook is enabled for that trigger point.

**Policy:** `USR-OSSI-DATA-CHANGE-HOOK`  
This is the master switch for rule execution across all trigger points.

## Configuration

Use the following format to enable a hook for a specific trigger point:

| `polcod` | `polvar` | `polval` | `rtstr1` | `rtnum1` |
|---|---|---|---|---|
| `USR-OSSI-DATA-CHANGE-HOOK` | `<TRIGGER_POINT>` | `0` | | `2` |


Setting `rtnum1` on each row controls whether the Rule Engine listens at that 
trigger point.

- Set `rtnum1 = 0` to disable.
- Set `rtnum1 = 1` to execute via a job.
- Set `rtnum1 = 2` to enable inline execution.

For example 

| `polcod` | `polvar` | `polval` | `rtstr1` | `rtnum1` |
|---|---|---|---|---|
| `USR-OSSI-DATA-CHANGE-HOOK` | `CAR_MOVE` | `UC_RULE_GRP` |`OSSI-CARMOV-CREATED` | `2` |

## Trigger Points

Each `polvar` value maps to a specific system event. Below are a few 
trigger points and their configuration for your help.

### Order & Shipment Events

| `polvar` | Description |
|----------|-------------|
| `OSSI-ORD-BEFORE-CRUD` | Fires before an order record is created or updated |
| `OSSI-ORDER-CREATED` | Fires after an order is successfully created |
| `OSSI-ORD_LINE-BEFORE-CRUD` | Fires before an order line is created or updated | 
| `OSSI-SHIPMENT-CREATED` | Fires after a shipment is created | `2` |
| `OSSI-CARMOV-CREATED` | Fires when a carrier movement record is created | 

### Inventory & Work Events

| `polvar` | Description | 
|----------|-------------|
| `OSSI-INVENTORY-STATUS-CHANGE` | Fires when inventory status is updated. When set to `0`, the create inventory trigger will not call hooks |
| `OSSI-PICK-RELEASE` | Fires during pick release and work execution |
| `OSSI-TRAILER-DISPATCHED` | Fires when a trailer is dispatched |


### Integration

| `polvar` | Description | 
|----------|-------------|
| `OSSI-INTEGRATION` | Controls hook execution for integration value mapping | 

---