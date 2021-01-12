# Testing a Spec

## Testing FAQs

### What's the best way to test my spec

1. Make sure Fig is on and autocomplete is working
2. Every time you make a change to your completion spec:
   - Go to a new line in your terminal
   - Type `cd`
   - Backspace repeatedly until the line is empty
   - Type the command for the completion spec as you would normally

### This is weird. Why do I do this?

Fig does "just-in-time" loading of completion specs. As you type a command into your Terminal, we work out what CLI tool you're using (e.g. `cd`, `git`, `brew`, ...) and load up the relevant completion spec from your `~/.fig/autocomplete` directory.

However, to be more efficient, if you use the same CLI tool that Fig has already loaded, we won't load it again i.e. if you do  `git add .` then immediately type  `git commit -m "hello world"` , we will load `git` the first time. The when you type the second command, because the `git` spec is already loaded, we don't reload it a second time.

Let's say you are testing a completion spec for a made up CLI tool called `foobar`. When you're testing the `foobar` completion spec, chances are you are typing `foobar` repeatedly. This means the `foobar` completion spec will stay in memory. By typing `cd` on a new line, you are loading up the `cd` completion spec. When you type in `foobar` after this, we will re-load up the `foobar` completion spec with all your new edits.

## **Where should I save my completion spec?**

Fig reads completion specs from the following folder: `~/.fig/autocomplete`

You can edit your spec there. Or you can see the **testing best practices** below for a smarter way that makes

## **How do I view the logs?**

Right click the popup window and click **Inspect Element.** It will open up Safari's web dev console

![](../assets/autocomplete/testing-a-spec/inspect.png)

## **My spec isn't showing up in autocomplete**

1. Is autocomplete working? Try going to a new line in the terminal and typing `git` or `cd` plus a space.

   1. If Fig pops up, autocomplete is working. Chances are it is a problem with your script. Make sure you have correct syntax. View the logs (above) for any errors.
   2. If Fig doesn't pop up, autocomplete has crashed 😬. Click to the Fig Icon (◧) in the mac status bar and toggle autocomplete on and off

   ![](../assets/autocomplete/testing-a-spec/menubar.png)

2. If Fig still doesn't work, restart Fig ( ◧ -> Restart Fig)

3. If Fig still doesn't work, message us in [Slack](https://figcommunity.slack.com/join/shared_invite/zt-fupa9n8g-sfHm8MyBn1DBaCj8SoIxSA#/) or email [hello@withfig.com](mailto:hello@withfig.com)

## **Fig isn't working. What are some debug steps**

View our support guide

[Fig User Manual](https://www.notion.so/Fig-User-Manual-e2858870edc44f8aa21843be79786a85)

# Helpful Hacks

**If you plan to push your completion spec publicly to our [withfig/autocomplete](https://github.com/withfig/autocomplete) github repo, read below.**

I like editing my spec in my local copy of the github repo so it's easy to push later and so it doesn't accidentally get overwritten.

1. Clone the public [withfig/autocomplete](https://github.com/withfig/autocomplete) git repo (I clone it to  `~/Desktop/public-autocomplete` below )

```bash
git clone <https://github.com/withfig/autocomplete.git> ~/Desktop/public-autocomplete
```

1. Edit your script from directly from the `specs` folder of the repo you just cloned above.
2. Add the following alias to your `~/.zshrc` or `~/.bashrc` files

```jsx
alias copy_autocomplete_scripts_over='cp ~/Desktop/public-autocomplete/specs/* ~/.fig/autocomplete/'
```

(Make sure to update the path to the cloned repo)

Now every time you make a change in the repo, run the `copy_autocomplete_scripts_over` command and all the scripts will overwrite whatever is in your `~/.fig/autocomplete` folder