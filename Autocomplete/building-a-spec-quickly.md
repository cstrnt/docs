# Building a Spec Quickly

Before reading on, please make sure you are familiar with our completion spec format

- [Getting Started with Autocomplete Specs](./getting-started)
- [API Reference](./api)

## Quick Summary

Your goal is to map a CLI tool to Fig's completion spec as quickly as possible.

The below guide should offers advice and hacks for

1. Where to get data (like commands, subcommands, options, descriptions etc) about a CLI tool
2. How to effective capture all the data a structured way (through scraping etc)
3. How to quickly format your structured data into a completion spec

If you have more ideas, please comment and let us know (we will integrate them) 🙂

## Where to get the data

### --help

Almost all modern CLI tools have `-h` or `--help` flag.

```bash
heroku --help
git --help

# Often works for subcommands too
heroku addons --help
git commit --help
```

![](/docAssets/autocomplete/building-a-spec-quickly/--help.png)

![](/docAssets/autocomplete/building-a-spec-quickly/--help2.png)

#### man pages

Many (but not all) CLI tools have a man page. Newer CLI tools (like heroku, aws etc) tend to use `--help` instead

```bash
man git
```

The **Synopsis** section gives you a good summary of the subcommands, options, and arguments.

- **Symbol meanings**
  - Angle brackets `< >` mean something is mandatory
  - Square brackets `[ ]` mean something is optional
  - Pipe `|` means OR
    - e.g. `-n | --dry-run` are the same thing
  - Ellipsis `...` means the argument is variadic, so the user can input infinite arguments

  ![](/docAssets/autocomplete/building-a-spec-quickly/variadic.png)

- **Options**

  - Brackets starting with `-` or `--` are options

- **Arguments**

  - Everything else contained within brackets is an argument e.g. `<repository>`
  - Anything after an equals `=` sign is an argument to an option

- **Other notes**

  - Arguments can be recursive e.g. for git push we have  `[<repository> [<refspec>...]]`

![](/docAssets/autocomplete/building-a-spec-quickly/recursive.png)

The **Options** section gives descriptions for all the options

![](/docAssets/autocomplete/building-a-spec-quickly/options.png)

#### tab completions

Bash and zsh have inbuilt completion by clicking tab.

We are obviously biased and think our completion is better, mostly because we can complete on many more things (like

You will have to disable Fig to make use of this trick.

Type in a command, hit tab, wait a few seconds, and if prompted, hit tab again

## How to get the data

**Web scraping**

You can search for CLI reference or manuals online, and scrape those sites for the relevant data. This method works best if the reference is presented in a structured, list-like format.

For example, with the [Git documentation](https://git-scm.com/docs/git), the options and command names, along with their descriptions, can be quickly scraped with a no-code scraper.

We've had success using https://webscraper.io/.

**Copy / paste**

- This is pretty obvious.
- Pushing it
