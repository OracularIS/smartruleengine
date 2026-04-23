# Delay Execution Policy

## What is the Delay Execution Policy?

The Delay Execution Policy postpones rule execution instead of processing it 
inline. When enabled, the system queues the rule and handles it at a later 
stage in the workflow.

:::info Policy Name
`DELAY-EXECUTION-WHEN-CALLED-FROM-INTEGRATOR`
:::


## When to Use It

Use this policy when:

- A rule is triggered from an integration process and immediate execution 
  would block or interfere with the integration flow
- Dependent processes need to complete before the rule logic runs
- Immediate execution is not required and deferral improves system performance


## Configuration

| `polcod` | `polvar` | `polval` | `rtstr1` | `rtnum1` |
|---|---|---|---|---|
| `DELAY-EXECUTION-WHEN-CALLED-FROM-INTEGRATOR` | `GLOBAL-MAP` | | | `1` |

| `rtnum1` | Description |
|---|---|
| `1` | Enables deferred execution for integration processes |

---
