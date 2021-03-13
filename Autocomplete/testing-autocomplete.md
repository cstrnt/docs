# Testing a Spec

## The Fig Linter

The [withfig/autocomplete](https://github.com/withfig/autocomplete) repo contains a linter program that can be used to validate your specs automatically. It returns syntax and type errors from your autocomplete spec.

To use the linter, run the following command from the root autocomplete folder.
`node linter.js specs/[specName].js`

To run the linter on ALL specs in the /specs folder, run
`node linter.js` or `npm test`.

Note that you'll need to run `npm install` to grab the right dependencies.

## What's the best way to test my spec?

1. Make sure Fig is on and autocomplete is working
2. Put your spec in the `~/.fig/autocomplete` directory (or symlink it there from wherever you are building it)
3. Test your spec automatically using the Fig linter
4. Test your spec manually in the terminal:
   - Go to a new line in your terminal
   - Type `cd`
   - Backspace repeatedly until the line is empty
   - Type the command for the completion spec as you would normally

## That's weird - Why do I have to type in `cd` to test? 

Fig caches completion specs on each load.  Typing in `cd` invalidates the cache by loading the `cd` completion spec.

Let's say you are building a completion spec for your CLI tool, `foobar`. When you type `foobar` into your Terminal, Fig loads the `foobar`completion spec. This spec will remain loaded until another one replaces it. No matter what changes you make to the `foobar` spec, these will not be displayed until you load another spec, then load up `foobar` again.

## Where should I save my completion spec?

Fig reads completion specs from the following folder: `~/.fig/autocomplete`

You can edit your spec there. Or you can edit it from anywhere and symlink it to that repo

```bash
ln -s /path/to/my/spec ~/.fig/autocomplete/
```


## How do I view the logs?

Right click the popup window and click **Inspect Element.** It will open up Safari's web dev console

![](/docAssets/autocomplete/testing-a-spec/inspect.png)



## My spec isn't showing up in autocomplete

- Is autocomplete working? Try going to a new line in the terminal and typing `git` or `cd` plus a space. 
   - If Fig pops up, autocomplete is working. Chances are it is a problem with your script. Make sure you have correct syntax. View the logs (above) for any errors. 
   - If Fig doesn't pop up, autocomplete has crashed 😬. Click to the Fig Icon (◧) in the mac status bar and toggle autocomplete on and off
![](/docAssets/autocomplete/testing-a-spec/menubar.png)

- If Fig still doesn't work, restart Fig ( ◧ -> Restart Fig)

- If Fig still doesn't work, message us in [Slack](https://figcommunity.slack.com/join/shared_invite/zt-fupa9n8g-sfHm8MyBn1DBaCj8SoIxSA#/) or email [hello@withfig.com](mailto:hello@withfig.com)


## Fig isn't working. What are some debug steps

View our support guide

[Fig User Manual](/docs/support/manual)



## Contributing

If you'd like to contribute, please fork our [withfig/autocomplete](https://github.com/withfig/autocomplete) github repo and submit a PR. 



Your spec will have to pass a linting test in GitHub actions and a quick security review by the Fig team before we merge it.

