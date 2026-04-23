# Context Policy

## What is a Context Policy?

A Context Policy defines the scope and criteria under which a rule is applied. 

It tells the Rule Engine which context variables to use when building the rule 
identifier, allowing rules to be targeted at specific combinations of warehouse, 
client, order type, and more.

Without a Context Policy, the Rule Engine has no way to narrow down which rules 
are relevant for a given transaction.

:::info
Context Policies are evaluated before rule execution. If the context does not 
match or the policy is not configured the rule is skipped.
:::

---

## Configuration Format

| `polcod` | `polvar` | `polval` | `rtstr1` | `rtnum1` |
|---|---|---|---|---|
| `USR-CTXT-OSSI-XXX` | `GLOBAL-MAP` | `<VARIABLE>` | `<expression>` | `<enabled/disabled>` |

- `polval` — the context variable being mapped (e.g. `WH_ID`, `CLIENT_ID`, `ORDTYP`)
- `rtstr1` — the expression used to build the value (leave blank for direct 
  context variable passthrough)
- `rtnum1` — policy enabled (1) or disabled (2)

---

## A few Context Policies

### USR-CTXT-OSSI-APPT-BEFORE-CRUD

Applies to appointment records before a CRUD operation. Builds the rule ID 
from warehouse, client, and order type.

| `polvar` | `polval` | `rtnum1` | `rtstr1` |
|---|---|---|---|
| `GLOBAL-MAP` | `WH_ID` | `1` | |
| `GLOBAL-MAP` | `CLIENT_ID` | `2` | |
| `GLOBAL-MAP` | `UC_RULE_ID` | `1` | `@wh_id \|\| '-' \|\| @client_id \|\| '-' \|\| @ordtyp` |
| `GLOBAL-MAP` | `UC_RULE_ID_WILD_CARD_01` | `1` | `@wh_id \|\| '-' \|\| @client_id \|\| '-XXXX'` |


### USR-CTXT-OSSI-APPT-CREATED

Applies to appointment records after creation. Builds the rule ID from 
warehouse only.

| `polvar` | `polval` | `rtnum1` | `rtstr1` |
|---|---|---|---|
| `GLOBAL-MAP` | `WH_ID` | `1` | |
| `GLOBAL-MAP` | `UC_RULE_ID` | `1` | `@wh_id` |
| `GLOBAL-MAP` | `UC_RULE_ID_WILD_CARD_01` | `1` | `'XXXX'` |

### USR-CTXT-OSSI-CAR_MOVE-BEFORE-CRUD

Applies to carrier movement records before a CRUD operation. Builds the rule 
ID from warehouse, client, and order type, same pattern as APPT-BEFORE-CRUD.

| `polvar` | `polval` | `rtnum1` | `rtstr1` |
|---|---|---|---|
| `GLOBAL-MAP` | `WH_ID` | `1` | |
| `GLOBAL-MAP` | `CLIENT_ID` | `2` | |
| `GLOBAL-MAP` | `ORDTYP` | `1` | |
| `GLOBAL-MAP` | `UC_RULE_ID` | `1` | `@wh_id \|\| '-' \|\| @client_id \|\| '-' \|\| @ordtyp` |
| `GLOBAL-MAP` | `UC_RULE_ID_WILD_CARD_01` | `1` | `@wh_id \|\| '-' \|\| @client_id \|\| '-XXXX'` |

---

### USR-CTXT-OSSI-CARMOV-CREATED

Applies to carrier movement records after creation.

| `polvar` | `polval` | `rtnum1` | `rtstr1` |
|---|---|---|---|
| `GLOBAL-MAP` | `WH_ID` | `1` | |
| `GLOBAL-MAP` | `UC_RULE_ID` | `1` | `@wh_id` |
| `GLOBAL-MAP` | `UC_RULE_ID_WILD_CARD_01` | `1` | `'XXXX'` |

---

### USR-CTXT-OSSI-CARMOV-STAGED

Applies to carrier movement records at staged status.

| `polvar` | `polval` | `rtnum1` | `rtstr1` |
|---|---|---|---|
| `GLOBAL-MAP` | `WH_ID` | `1` | |
| `GLOBAL-MAP` | `UC_RULE_ID` | `1` | `@wh_id` |
| `GLOBAL-MAP` | `UC_RULE_ID_WILD_CARD_01` | `1` | `'XXXX'` |


### USR-CTXT-OSSI-CONSOLIDATE-SHIPMENT-LINES

Applies during shipment line consolidation.

| `polvar` | `polval` | `rtnum1` | `rtstr1` |
|---|---|---|---|
| `GLOBAL-MAP` | `UC_RULE_ID` | `1` | `@wh_id` |


## Wildcard Reference

You can create you own like shown below:

| Pattern | Matches |
|---|---|
| `WH_ID-CLIENT_ID-ORDTYP` | Exact: specific warehouse, client, and order type |
| `WH_ID-CLIENT_ID-XXXX` | Any order type for this warehouse and client |
| `XXXX-CLIENT_ID-XXXX` | Any warehouse and order type for this client |
| `WH_ID-XXXX-XXXX` | Any client and order type for this warehouse |
| `XXXX-XXXX-XXXX` | Catch-all |

---
