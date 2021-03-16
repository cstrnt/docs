# Getting Started with Autocomplete Specs

Autocomplete specs add support for a CLI tool to Fig's autocomplete. They serve two purposes:

**1. Define a CLI tool in a structured tree-like representation.**
  - Mapping a user's Terminal input to this defined tree structure gives us the context on the user's input. This lets us accurately generate suggestions.
  - *e.g. we will generate very different suggestions if a user types `git` versus `git commit -`*


**2. Contain Content Completion specs provide content (like descriptions, icons etc) for the suggestions that are rendered to the user.**
  - If instructions on how to generate suggestions (like get all the files in this specific folder)
  - i.e. your description of the `-m` option in `git commit -m` is what will displayed to the user!


```ts
export const completion:Fig.Spec = { // Command Object
  name: "git",
  description: "the stupid content tracker",
  subcommands: [ ... ], // Array of Command Objects 
  options: [ ... ], // Array of Option Objects
  args: [ ... ], // Array of Arg Objects
}
```

- To start building your own spec, see [Building Your First Autocomplete Spec](/docs/autocomplete/building-a-spec).
- Looking to dive deeper into everything you can do with specs? Check out the [API Reference](/docs/autocomplete/api).
- Already built a spec and need to test it out? See [Testing Autocomplete](/docs/autocomplete/testing-autocomplete).