# Key Components 

## Smart Rules 

Smart are value-determination rules used to compute and assign dynamic values to system variables based on evaluated conditions. They act as a configurable alternative to hardcoded decision log.

### Purpose
Smart Rules are used to:

- Determine system values dynamically at runtime
- Replace static configuration tables and hardcoded logic
- Simplify complex decision matrices
- Enable business users to adjust behavior without code changes

### Behavior Model

Smart Rules follow a decision-first model, where each rule evaluates a condition and returns a corresponding value.

- Rules are grouped under a rule subgroup
- Each rule contains:
    - A condition (uc_rule_expr)
    - A resulting value (uc_rule_value)
- Only enabled rules participate in execution

### Sequential Evaluation Logic

Smart Rules are evaluated in a top-down sequential order:

1. The first rule in the group is evaluated
2. If the condition is false, the next rule is checked
3. If the condition is true, evaluation stops immediately
4. The corresponding value is returned

## Conditional Rules

Conditional Rules are action-execution rules that trigger specific system actions when defined conditions are met. 

Unlike Smart Rules, they do not return values but execute workflows.

These rules function similarly to pre- and post-processing triggers within system workflows.

### Purpose

Conditional Rules are used to:

- Trigger business workflows based on system events
- Functions similarly to pre- and post-processing triggers within  system workflows

### Action-Based Execution

Conditional Rules operate on an event-action model:

- A condition is evaluated
- If true, one or more actions are executed
- Actions are executed sequentially
- Each action can modify system state or trigger external processes

---