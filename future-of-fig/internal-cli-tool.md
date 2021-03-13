# Build your own CLI

>🚨 This is currently unsupported, but is in Fig's product roadmap. We built an early prototype of it and plan to add full support in the future.

Fig makes it easy to visually build your own Command Line Interface (CLI) for yourself, your team, and your company. 

A CLI built with Fig lets you directly execute scripts. For users who often don't remember input parameters, flags, or commands, it lets you build an [interactive runbook ]()into the CLI. This makes traditional command line interfaces more discoverable, approachable, and interactive. 

## **How can I get started?**

1. Navigate to the directory where you want to save your CLI (e.g. your scripts folder in a shared repo)
2. Run [`fig build`]() to visually create and edit your CLI toolThis will create a .fig file in that folder
3. Add the directory from Step 1 where your .fig file is saved to your [$FIGPATH](). You do this in [Settings](). Make sure your teammates do the same
4. Run `fig CMD SUBCOMMAND` where CMD is the name of your .fig file, and where SUBCOMMAND is a command you defined in `fig build`. Your teammates can do this too 😀

`fig build`/build-a-cli/fig-build

![img](/docAssets/future-of-fig/internal-cli-tool/figBuild.png)

## What is a .fig file?

A .fig file is the blueprint for your CLI tool. It is a JSON stringified object that contains the mapping for all of your subcommands. 

## How should I name my .fig file?

The name of your .fig file (e.g. `ACME.fig`) defines the root command used to access the subcommands you defined.

e.g. If I had a file named ACME.fig with a subcommand called `deploy`, I could access it by running `fig ACME deploy`

## How do I share this CLI tool with my team?

1. You can host the .fig file with Fig (coming soon)
2. You can put the .fig file in a shared repository
3. Make sure your teammates add their local path to that shared repo to their [$FIGPATH]()