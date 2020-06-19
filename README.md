# Crossbeam Engineer Challenge

`crossbeam.sibilant` contains my solution to the [Crossbeam Engineer Challenge](https://gitlab.com/snippets/1967460), the original examples, and some additional examples that cover more cases.

The `determine-order` function accepts `tasks` and `chosen-tasks` as arguments. It then defines a function called `add-tasks`, which we will return to. Next, it declares an empty object called `dependencies` and populates it with the data from `tasks` in a way that makes looking up dependencies easier. It then passes `chosen-tasks` and `dependencies` to `add-tasks`.

`add-tasks` accepts `chosen-tasks`, `dependencies`, and `sorted-tasks` as arguments. The first time it is called, it does not receive `sorted-tasks`, so it defaults to an empty array. It then iterates over `chosen-tasks`. Inside the loop, it checks to see if the current `chosen-task` is already in `sorted-tasks`. If it is not, it calls `add-tasks` again, using the current `chosen-task`'s dependencies as the next list of tasks to process. It adds the returned tasks and the current `chosen-task` to `sorted-tasks`. When it is done iterating over `chosen-tasks`, it returns `sorted-tasks`. It continues to recurse through all of the dependencies until it reaches tasks that have no dependencies.

## Assumptions

`determine-order` makes the following assumptions:

1. `tasks` will be an array, containing objects that each have `task` (a string) and `depends` (an array of strings or an empty array)
2. Each `task` in `tasks` will be unique
3. In `tasks`, each string in `depends` is also used as `task` in another object
4. Within a single `tasks` object, `depends` must not contain the value for `task` (causes an infinite loop)
5. `chosen-tasks` will be an array of strings
6. Each string in `chosen-tasks` will equal `task` for one object in `tasks`

These problems could be protected against in the code, but I chose not to for clarity's sake.
