## Quickstart 🚀

Set up:

```bash
brew install task
git clone https://github.com/fredrikaverpil/poc-tasks-gitrepo.git
cd poc-tasks-gitrepo
```

List all available tasks:

```bash
task --list
```

List all tasks, including "internal" tasks:

```bash
task --list-all
```

Run task:

```bash
task <task-name>
```

## Demo

### Tasks defined in this git repo

A default task was defined in this repo's `Taskfile.yml` and can be executed like this:

```bash
task

# or with...

task default
```

Another example, showcasing tasks using a sub-task:

```bash
task top-task
```

### Include tasks from another local `Taskfile.yml`

Example:

```yml
version: "3"

includes:
  your-namespace: ~/dotfiles/Taskfile.yml
```

Run tasks from this file like so (note that this is not implemented in this POC repo):

```bash
task your-namespace:task-name
```

### Include tasks from another remote git repo

⚠️ requires the `TASK_X_REMOTE_TASKFILES=1` environment variable to be set, as this is still an [experimental feature](https://taskfile.dev/experiments/remote-taskfiles/).

Example:

```yml
version: "3"

includes:
  public: https://raw.githubusercontent.com/fredrikaverpil/poc-tasks/main/Taskfile.yml
```

Any language can be used to implement the actual logic invoked by a task (in this example, Go):

```bash
task public:poc-app
```

Ciapp can be wrapped:

```bash
# run 'ciapp lint'
task public:ciapp -- lint
```

### Good to be aware of

- Nested remote Taskfiles are supported.
- Token-based authentication is being worked on for private repos and e.g. GitHub Actions: https://github.com/go-task/task/discussions/1420#discussioncomment-7752097
- SSH authentication might come later.
- You can keep a local `~/Taskfile.yml` in which you invoke your own scripts/binaries. Use `task --global ...` to toggle.
