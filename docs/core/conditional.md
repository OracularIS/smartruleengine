# Conditional Rules

## What is a Conditional Rule?

A Conditional Rule is an action-execution rule. It evaluates conditions and, 
when met, executes one or more predefined actions in sequence.

Unlike Smart Rules, Conditional Rules do not return a value. They trigger 
something to happen.


## How It Works

Conditional Rules follow an **event-action model**:

1. All enabled rules in the group are evaluated
2. For each rule whose condition is satisfied, its actions execute in order
3. Evaluation continues to the next rule unless explicitly stopped
4. Execution halts early if an action returns `uc_abort_conditional_rules = 1`
5. Execution also stops if an error occurs.


## Core Attributes

| Attribute | Description |
|---|---|
| `uc_rule_subgrp_id` | Defines the rule group this rule belongs to |
| `uc_rule_id` | Unique identifier for the rule. Supports wildcard `XXXX` |

---

### Execution Controls

| Control | Description |
|---|---|
| `uc_abort_conditional_rules = 1` | Returned by an action to stop all further rule processing |
| `noop` command | Used to explicitly define no action for a rule |


### Rule Groups

Conditional Rules are organised into groups tied to specific system events.

| Rule Group | Trigger Point |
|---|---|
| `OSSI-ORDER-CREATED` | Triggered after order creation |
| `OSSI-SHIPMENT-CREATED` | Triggered after shipment creation |
| `OSSI-PICK-RELEASE` | Work execution logic |
| `OSSI-INVENTORY-STATUS-CHANGE` | Inventory status updates |
| `OSSI-TRAILER-DISPATCHED` | Trailer lifecycle events |

---

## Example

**Scenario:**  After an order is created at your warehouse, the system needs to 
check if it is an international order. If it is, trigger a compliance check 
workflow and stop processing further rules.

| `uc_rule_subgrp_id` | `uc_rule_id` | Condition | Action |
|---|---|---|---|
| `OSSI-ORDER-CREATED` | `INTL-COMPLIANCE` | `ship_to_country != 'US'` | Run compliance check command, return `uc_abort_conditional_rules = 1` |
| `OSSI-ORDER-CREATED` | `DOMESTIC-NOTIFY` | `ship_to_country = 'US'` | Send domestic processing notification |

In this example, if the order is international, the compliance action fires and 
`uc_abort_conditional_rules = 1` halts evaluation — the domestic notification 
rule never runs.

---

