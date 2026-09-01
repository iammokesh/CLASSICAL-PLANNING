## ExpNo:10 Implementation of Classical Planning Algorithm
## Algorithm or Steps Involved:

1.Define the initial state
2.Define the goal state
3.Define the actions
4.Find a <b>plan</b> to reach the goal state
5.Print the plan

## CODE:
```python
def is_goal_state(current_state, goal_state):
    return all(
        current_state.get(key) == value
        for key, value in goal_state.items()
    )


def is_applicable(current_state, precondition):
    return all(
        current_state.get(key) == value
        for key, value in precondition.items()
    )


def apply_action(current_state, action_effect):
    new_state = current_state.copy()
    new_state.update(action_effect)
    return new_state


def find_plan(initial_state, goal_state, actions):
    queue = [(initial_state, [])]
    visited_states = set()

    while queue:
        current_state, partial_plan = queue.pop(0)

        if is_goal_state(current_state, goal_state):
            return partial_plan

        state_tuple = tuple(sorted(current_state.items()))

        if state_tuple in visited_states:
            continue

        visited_states.add(state_tuple)

        for action in actions:
            if is_applicable(
                current_state,
                actions[action]['precondition']
            ):
                next_state = apply_action(
                    current_state,
                    actions[action]['effect']
                )

                queue.append(
                    (next_state, partial_plan + [action])
                )

    return None


n = int(input("Enter number of objects: "))

initial_state = {}

print("Enter initial state:")

for i in range(n):
    obj = input("Object: ")
    position = input("Position: ")
    initial_state[obj] = position


goal_state = {}

print("\nEnter goal state:")

for i in range(n):
    obj = input("Object: ")
    position = input("Position: ")
    goal_state[obj] = position


m = int(input("\nEnter number of actions: "))

actions = {}

for i in range(m):
    print("\nAction", i + 1)

    name = input("Action name: ")

    p = int(input("Number of preconditions: "))
    precondition = {}

    for j in range(p):
        key = input("Precondition object: ")
        value = input("Precondition position: ")
        precondition[key] = value

    e = int(input("Number of effects: "))
    effect = {}

    for j in range(e):
        key = input("Effect object: ")
        value = input("Effect position: ")
        effect[key] = value

    actions[name] = {
        'precondition': precondition,
        'effect': effect
    }


plan = find_plan(initial_state, goal_state, actions)

if plan:
    print("\nPlan:", plan)
else:
    print("\nNo plan exists.")
```



# Example - 1
```
initial_state = {'A': 'Table', 'B': 'Table'}
goal_state = {'A': 'B', 'B': 'Table'}

actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_Table': {'precondition': {'A': 'Table', 'B': 'B'}, 'effect': {'B': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)
```

# Example - 2
```
initial_state = {'A': 'Table', 'B': 'Table', 'C': 'Table'}
goal_state = {'A': 'B', 'B': 'C', 'C': 'Table'}

actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_C': {'precondition': {'A': 'B', 'B': 'Table', 'C': 'Table'}, 'effect': {'B': 'C'}},
    'move_C_to_Table': {'precondition': {'A': 'B', 'B': 'C', 'C': 'C'}, 'effect': {'C': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)
```
# Output:
<img width="497" height="69" alt="image" src="https://github.com/user-attachments/assets/1393448f-ad72-4d3b-b29f-6e910b4d44f5" />

## RESULT:
The program was Executed Susccesfully.
