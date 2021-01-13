# Getting Started with Autocomplete Specs

Fig takes a user's terminal input, splits it into an abstract syntax tree (AST), maps this AST to the completion-spec, works out the range of possibilities of what the user could input next (these possibilities are called suggestions), and renders the suggestions to the user.

This is a lot of steps. The only thing you need to worry about is making a good completion spec.

Fig's completion specs serve two purposes. They

1. **Define a CLI tool in a structured tree-like representation.** Mapping a user's Terminal input to this defined tree structure gives us the context on the user's input. This lets us accurately generate suggestions.

   *e.g. we will generate very different suggestions if a user types `git` versus `git commit -`*

2. **Contain Content** Completion specs provide content (like descriptions, icons etc) for the suggestions that are rendered to the user. If instructions on how to generate suggestions (like get all the files in this specific folder)

i.e. your description of the `-m` option in `git commit -m` is what will displayed to the user!

```jsx
var completionSpec = { // Command Object
    name: "git",
    description: "the stupid content tracker",
    subcommands: [ // Array of Command Objects
        {
            name: "commit",
            description: "Record changes to the repository",
            options: [ ... ] 
        },
        { ... }
    ],
    options: [ // Array of Option Objects
        {
            name: "--version",
            description: "Print git's current version"
        },
        { ... }
    ]
    args: [ ... ], // Array of Arg Objects
    additionalSuggestions: [ ... ] // Array of Suggestion Objects
}
```

The fastest way to learn is by looking at examples. We suggest looking at some of the completion specs for commands you know well, like [git](https://github.com/withfig/autocomplete/blob/master/specs/git.js) or [npm](https://github.com/withfig/autocomplete/blob/master/specs/npm.js). You should be able to pick up the format pretty quickly.

**All current specs**: [withfig/autocomplete](https://github.com/withfig/autocomplete)

