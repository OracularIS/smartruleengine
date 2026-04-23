# Smart Rules vs Conditional Rules

## At a Glance

| | Smart Rules | Conditional Rules |
|---|---|---|
| **Purpose** | Determine a value | Execute an action |
| **Question it answers** | "What value should this field be?" | "What should happen next?" |
| **Evaluation** | Stops at first match | Evaluates all enabled rules |
| **Output** | A value assigned to a variable | An action performed |
| **Can be aborted?** | Not applicable | Yes, via `uc_abort_conditional_rules = 1` |

## Can They Work Together?

Yes — and this is common in practice. A single trigger point can have both a 
Smart Rule and a Conditional Rule active at the same time. The execution order 
depends on the trigger type:

| Trigger Type | Execution Order |
|---|---|
| **Before CRUD** | Smart Rule runs first → value published → Conditional Rule actions execute |
| **At Created** | Conditional Rule actions run first → Smart Rule publishes value → table updated |

This means you can use a Smart Rule to determine a value **and** a Conditional 
Rule to act on the same event — they complement each other.

---
