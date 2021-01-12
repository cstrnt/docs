# Building a Spec Quickly



Before reading on, please make sure you are familiar with our completion spec format

[Getting Started with Autocomplete Specs](https://www.notion.so/Getting-Started-with-Autocomplete-Specs-9ddc5213614c44108b2fedf64b8d0d00)

[API](https://www.notion.so/API-abe0f08b4f764a5d8e6b802063af61ed)

# Quick Summary

Your goal is to map a CLI tool to Fig's completion spec as quickly as possible.

The below guide should offers advice and hacks for

1. Where to get data (like commands, subcommands, options, descriptions etc) about a CLI tool
2. How to effective capture all the data a structured way (through scraping etc)
3. How to quickly format your structured data into a completion spec

If you have more ideas, please comment and let us know (we will integrate them) 🙂

# 1. Where to get the data

## --help

Almost all modern CLI tools have `-h` or `--help` flag.

```bash
heroku --help
git --help

# Often works for subcommands too
heroku addons --help
git commit --help
```

![](../assets/autocomplete/building-a-spec-quickly/--help.png)

![](../assets/autocomplete/building-a-spec-quickly/--help2.png)

## man pages

Many (but not all) CLI tools have a man page. Newer CLI tools (like heroku, aws etc) tend to use `--help` instead

```bash
man git
```

The **Synopsis** section gives you a good summary of the subcommands, options, and arguments.

- **Symbol meanings**

  - Angle brackets `< >` mean something is mandatory

  - Square brackets `[ ]` mean something is optional

  - Pipe 

    ```
    |
    ```

     means OR

    - e.g. `-n | --dry-run` are the same thing

  - Ellipsis 

    ```
    ...
    ```

     means variadic ie the user can continually input arguments forever

    - e.g.

      ![](../assets/autocomplete/building-a-spec-quickly/variadic.png)

- **Options**

  - Brackets starting with `-` or `--` are options

- **Arguments**

  - Everything else contained within brackets is an argument e.g. `<repository>`
  - Anything after an equals `=` sign is an argument to an option

- **Other notes**

  - Arguments can be recursive e.g. for git push we have  `[<repository> [<refspec>...]]`

![](../assets/autocomplete/building-a-spec-quickly/recursive.png)

The **Options** section gives descriptions for all the options

![](../assets/autocomplete/building-a-spec-quickly/options.png)

## tab completions

Bash and zsh have inbuilt completion by clicking tab.

We are obviously biased and think our completion is better, mostly because we can complete on many more things (like

You will have to disable Fig to make use of this trick.

Type in a command, hit tab, wait a few seconds, and if prompted, hit tab again

# 2. How to get the data

## scraping

https://webscraper.io/

## Copy / paste

- This is pretty obvious.
- Pushing it

# 3. How format the data into a completion spec

## Multi-cursor