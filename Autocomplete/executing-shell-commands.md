# Executing Shell Commands



### Where do I define a shell command to execute?

Shell commands are executed by generators.

- **Script as a String**: The `script` prop. is executed
- **Script as a Function**: The output of the `script` prop function
- **CustomFunction**: Any time `await runFigCommand("foo")`

[Generators](https://www.notion.so/Generators-3f8601593c1c4c58a497adbfd658a11d)

### How are shell commands executed

Let's say `{{cmd}}` is the command you want to execute, Fig will execute your command

```bash
( cd /path/to/current/directory; {{cmd}} | cat )
```

- `/path/to/current/directory` → the current working directory of the user. e.g. if they typed pwd

### Advanced Notes

- We execute all of your commands in a pseudo-terminal running a login-shell
  - of the user's default shell. (e.g. if the user's default shell is zsh, we run it in a zsh shell).
- We execute commands inside a subshell to contain the environment.
- We pipe into cat to remove escape characters (like color codes) from the output