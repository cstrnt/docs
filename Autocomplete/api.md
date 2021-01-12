On this page

- Root Object
- Suggestion Object
- Subcommand Object
- Option Object
- Arg Object
- Generator Object

### Root Object

```jsx
// Must be "var" NOT "let" or "const")
// Must be "completionSpec" 
var completionSpec = { // this is a Subcommand Object
	...
}
```

### Suggestion Object

| Prop Name   | Type                       | Required | Default                                                      | Description |
| ----------- | -------------------------- | -------- | ------------------------------------------------------------ | ----------- |
| name        | string or array of strings | - [ x ]  |                                                              |             |
| displayName | string                     | - [ ]    | the name prop                                                |             |
| insertValue | string                     | - [ ]    | the name prop                                                |             |
| description | string                     | - [ ]    | null                                                         |             |
| type        | string                     | - [ ]    | null                                                         |             |
| icon        | string                     | - [ ]    | auto-generated based on type prop. If type doesn't exist, will be ? |             |

### Subcommand Object

| Prop Name             | Type                               | Required | Default             | Description |
| --------------------- | ---------------------------------- | -------- | ------------------- | ----------- |
| name                  | string or array of strings         | - [ x ]  |                     |             |
| displayName           | string                             | - [ ]    | the name prop       |             |
| insertValue           | string                             | - [ ]    | the name prop       |             |
| description           | string                             | - [ ]    | null                |             |
| subcommands           | array of Subcommand objects        | - [ ]    |                     |             |
| icon                  | string                             | - [ ]    | the subcommand icon |             |
| options               | array of Option objects            | - [ ]    |                     |             |
| args                  | Arg object or array of Arg objects | - [ ]    |                     |             |
| additionalSuggestions | array of Suggestion objects        | - [ ]    |                     |             |



### Option Object

| Prop Name   | Type                               | Required | Default | Description |
| ----------- | ---------------------------------- | -------- | ------- | ----------- |
| name        | string or array of strings         | - [ x ]  |         |             |
| displayName | string                             | - [ ]    |         |             |
| insertValue | string                             | - [ ]    |         |             |
| description | string                             | - [ ]    |         |             |
| args        | Arg object or array of Arg objects | - [ ]    |         |             |
| icon        | string                             | - [ ]    |         |             |

**Note:** We rely on Arg objects to map what the user has typed to a completion spec. e.g. if you were building the git completion spec, under `git commit` you would specify an option for `-m, --message`.

presence of an Arg object in a Subcommand or Option object will signal that the given subcommand or option will take an arg. It is important to specify it, even if you don't fill in the details (literally do `args: {},` ) otherwise the parsing will be messed up.



### Arg Object

| Prop Name   | Type                                            | Required | Default                                                      | Description                             |
| ----------- | ----------------------------------------------- | -------- | ------------------------------------------------------------ | --------------------------------------- |
| name        | string                                          | - [ ]    |                                                              |                                         |
| displayName | string                                          | - [ ]    | the name prop                                                |                                         |
| insertValue | string                                          | - [ ]    | the name prop                                                |                                         |
| description | string                                          | - [ ]    | null                                                         |                                         |
| suggestions | array of strings or array of Suggestion objects | - [ ]    | null                                                         |                                         |
| icon        | string                                          | - [ ]    | auto-generated based on type prop. If type doesn't exist, will be ? |                                         |
| template    | string                                          | - [ ]    |                                                              | Must be either "filepaths" or "folders" |
| generators  | Generator object or array of Generator objects  | - [ ]    |                                                              |                                         |

**Note**: Nothing is required in an Arg object. The presence of it in a Subcommand or Option object will signal that the given subcommand or option will take an arg. It is important to specify it, even if you don't fill in the details (literally do `args: {},` ) otherwise the parsing will be messed up.

### Generator Object

| Prop Name                 | Type                                                         | Required | Default | Description                             |
| ------------------------- | ------------------------------------------------------------ | -------- | ------- | --------------------------------------- |
| template                  | string                                                       | - [ ]    |         | Must be either "filepaths" or "folders" |
| filterTemplateSuggestions | function * Input: array of Suggestion objects * Output: array of Suggestion objects | - [ ]    |         |                                         |
| script                    | string OR function function * Input: array of strings * Output: string | - [ ]    |         |                                         |
| splitOn                   | string                                                       | - [ ]    |         |                                         |
| postProcess               | function * Input: string * Output: array of Suggestion objects | - [ ]    |         |                                         |
| custom                    | async function  * Input: array of strings * Output: array of Suggestion objects | - [ ]    |         |                                         |
| trigger                   | string or function function * Inputs: string, string  * Output: boolean | - [ ]    |         |                                         |
| filterTerm                | string or function function * Input: string * Output: string | - [ ]    |         |                                         |

At least one of `template`, `script`, or `custom` are **required**. Only one of these three props is allowed per generator.

Learn more:

[Generators](./generators.md)