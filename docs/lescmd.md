# LES CMD Table

## What is the LES CMD Table?

The LES CMD table is a supporting data table used by the Rule Engine to 
fetch and store extended information that is not directly available in the rule 
context. 

It enables rules to operate on richer datasets by providing custom 
views and additional context variables at execution time.


## When It Is Used

The LES CMD table is queried during the LES CMD Execution step, which occurs 
early in every rule execution flow, after the Context Policy check and before 
rule criteria are evaluated.

This means any data fetched via LES CMD is available to both condition expressions 
and value definitions within the rule.



## Operation Types

The table supports two operation modes:

### `table_data_xxx`

Operates at the **table level**. Applied to the overall dataset, used when data 
needs to be fetched or processed in relation to the entire table rather than a 
specific action.

### `cmd_action_xxx`

Operates at the **action level**. Triggered in relation to specific actions,
used when data needs to be retrieved or handled for a particular event.


## Table Structure

:::note
The full LES CMD table data was not provided at the time of writing. 
Add the table rows here once confirmed.
:::

| Column | Description |
|---|---|
| `cmd_id` | Identifier for the command |
| `cmd_typ` | Type — `table_data_xxx` or `cmd_action_xxx` |
| `cmd_text` | The MOCA command or expression to execute |

---