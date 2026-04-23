# Smart Rules

## What is a Smart Rule?

A Smart Rule is a value-determination rule. It evaluates a set of conditions 
in order and returns the first matching value.

Think of it as a configurable lookup table that can think — instead of hardcoding 
"if carrier is X, set priority to Y", you define that logic as a rule that can be 
updated without touching code.


## How It Works

Smart Rules follow a **decision-first model**:

1. Rules in the group are evaluated top-down in sequence
2. Each rule checks its condition (`uc_rule_expr`)
3. The first rule whose condition evaluates to true wins
4. Its value (`uc_rule_value`) is published to the system
5. Evaluation stops — no further rules are checked

This means rule order matters. More specific conditions should always sit 
above more general ones.


## Core Attributes

| Attribute | Description |
|---|---|
| `uc_rule_subgrp_id` | Identifies which rule group this rule belongs to |
| `uc_rule_expr` | The condition to evaluate |
| `uc_rule_value` | The value to return if the condition is true |


### Condition Types (`uc_rule_expr`)

| Type | Format | Example |
|---|---|---|
| MOCA expression | Plain context variable expression | `trntyp = 'OUTBOUND'` |
| MOCA command block | Wrapped in `{ }`, must return `1` (true) or `0` (false) | `{ publish data where result = 1 }` |

---

### Value Types (`uc_rule_value`)

| Type | Format | Example |
|---|---|---|
| Literal | Plain value | `HIGH` |
| Expression | Wrapped in `[[ ]]` | `[[trntyp]]` |
| MOCA command block | Wrapped in `{ }` | `{ get priority where ... }` |



### Rule Groups

Smart Rules are organised into groups, each tied to a specific trigger point.

| Rule Group | Trigger Point |
|---|---|
| `OSSI-ORD-BEFORE-CRUD` | Pre-order creation logic |
| `OSSI-ORDER-CREATED` | Post-order processing |
| `OSSI-ORD_LINE-BEFORE-CRUD` | Pre-order line logic |
| `OSSI-INTEGRATION` | Integration value mapping |
| `OSSI-PICK-RELEASE` | Pick release value determination |


### Example

**Scenario:** You need to automatically assign a shipment priority 
based on order type. Express orders get `HIGH`, standard orders get `NORMAL`, 
and everything else defaults to `LOW`.

| `uc_rule_subgrp_id` | `uc_rule_expr` | `uc_rule_value` |
|---|---|---|
| `OSSI-ORD-BEFORE-CRUD` | `ordtyp = 'EXPRESS'` | `HIGH` |
| `OSSI-ORD-BEFORE-CRUD` | `ordtyp = 'STANDARD'` | `NORMAL` |
| `OSSI-ORD-BEFORE-CRUD` | `1 = 1` | `LOW` |

---
