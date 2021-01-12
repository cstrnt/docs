# Generators

## Quick Summary

Generators let you run shell commands on the user's device to *generate s*uggestions for arguments

- There are 4 types of generators (see below)

- Fig runs all shell commands in a separate login-shell at the current working directory of the user's terminal

  [Executing Shell Commands](./executing-shell-commands.md)

- Generators are defined in the `generators` property of an Argument object.

  - The `generators` property can be a single Generator object or an array of Generator objects.

### Examples

- `cd [folder]`
  - `cd` takes one argument: a single folder
    - Arg object 1: A generator that runs  `ls` to get the list of folders at the user's current directory
- `git push [remote] [branch]`
  - `git push` takes two arguments: a remote repo and a branch
    - Arg object 1: Include a generator that runs `git remote` as a script
    - Arg object 2: Include generator that runs `git branch` as a script

# Types of Generators

There are 4 types of generators. At the end of the day, they all give you the ability to define what shell command(s) to run. Then given that output, parse it however you'd like to produce Suggestion objects.

They types of Generator are listed below in order of customisability.

[Generator Types Summary](https://www.notion.so/1501f31d39724506a0a7b05501be650c)

We would say the vast majority of Generators you make will be using **Templates** and/or **Script as a String**

## Templates

Filepaths or folders are very common arguments for subcommands. e.g.

- `git add [file or folder path]`
- `cd [folder path]`
- `open [file or folder path]`
- `ls -l [file or folder path]`

Because it's so common, Fig has predefined these arguments for you as a template.

```jsx
// Define templates inside generators in order
// to use the filterTemplateSuggestions function

args: {
	generator: {
		**template**: "filepaths",
		**filterTemplateSuggestions**: (suggestions) => {       //optional
				var jsOnly = suggestions.filter((elm) => return elm.endsWith(".js"))
				return jsOnly
		}
}

**OR**

// Define templates directly underneath args if you don't need to filter
// This also looks nicer and is easier to read
args: {
		**template**: "filepaths",
}
```

Properties

| Property                  | Data Type                                                    | Description                                                  |
| ------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| template                  | string                                                       | One of: <br />- "filepaths": shows all files AND folders at current working directory (like running ls). <br />- "folders": only shows folders in current working directory (like running ls then filtering on.<br />These template also allow users to type / at the end of a directory and Fig will run show the files/folders in the new subdirectory. |
| filterTemplateSuggestions | function(suggestions: SuggestionObject[ ]): SuggestionObject | **[Optional]**<br /><br />A function that let's you filter the array of Suggestion objects output by the template. e.g. if you only wanted to show files ending in `.js` you could use a filter method inside.<br /><br />**Function Parameters 1**<br />. suggestions: an array of Suggestion objects that was output by the template <br /><br />**Output**<br />an array of Suggestion objects that was output by the template |

**Notes & Hints**

- the `filterTemplateSuggestions` is only available if you define the the `template` inside a generator object
- if you define `template` outside a generator object, this will override
- If you don't plan on using `filterTemplateSuggestions`, we recommend defining `template` outside the generator object. It is easier to read inside the spec.
- Both templates have a trigger attached to them which cause Fig to re-run the suggestion object when a user types a `"/"`
  - e.g. if a user is in their Home (~) directory and inserts `cd Desktop/` Fig will render suggestions from the Desktop directory

## Script as a String

If you're suggesting something other than files or folders, we recommend using this. This let's you run a mini-script / command on the user's computer. The script runs in the user's current working directory and in the same shell. It's as if the user typed the command themselves.

The output from the script you specify is then converted to Suggestion objects. We can do this for you with `splitOn` or you can process the output yourself with `postProcess`

```jsx
args: {
		script: "git branch"

		splitOn: "\\n",
		// **OR**
		postProcess: (scriptOutput: string) => {

			var arr = scriptOutput.split("\\n")
			
			// return an array of Suggestion Objects
			return arr.map((elm) => {
					return {
						name: elm,
						icon: "🌱"
					}
			})
			
		},

		
		// [optional]
		trigger: (after: string, before: string) {
			if before.countSlash !== after.countSlash return true
			else return false
		}
}
```

Properties

| Property    | Data Type                                                    | Description                                                  |
| ----------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| script      | string                                                       | The shell command to execute in the user's current working directory. The output is a string. It is then converted into an array of Suggestion objects using `splitOn` or `postProcess`<br /><br /> e.g. git branch → show all the remote git repos available |
| postProcess | function(scriptOutput: string): SuggestionObject { } <br /><br />**Input**: output of executing script <br />**Output**: array of Suggestion objects | **[Must specify one of postProcess or splitOn]** <br /><br />Define a function that takes a single input: the output of executing script. This function then return an array of Suggestion objects that will be rendered by Fig.  <br /><br />**Examples** <br />If `script` outputs data separated cleanly by newlines, or commas... <br />- split the input on new lines <br />- map or filter over your new array <br />- if each line had columns, split it again during the map<br />If `script` outputs json data,  use JSON.parse.<br /><br />**Other ideas** - use try/catch and return an empty array if there's an error |
| splitOn     | string                                                       | [Must specify one of  splitOn OR postProcess] <br /><br />As splitting the output of `script` is such a common use case for `postProcess`, we build the `splitOn` property. Simply define a string to split the output of script on (e.g. `","` or `"\n"` and Fig will do the work of the `postProcess` prop for you.  <br /><br />This is a simple and fast method to generate suggestions. If you want any more control over the parsing (like filtering) or you want more control over the UI, use `postProcess`. <br /><br />e.g. if the script was `git branch`, specifying splitOn = \n would split the output on new lines and automatically create a Suggestion object for each element. |
| trigger     | function                                                     | **[Optional]** See [Trigger]()                               |
| filterTerm  | function or string                                           | **[Optional]** See [Filter Term]                             |

**Notes & Hints**

- In `script`: You can chain multiple commands together in the one string and then use javascript to combine  their output. e.g. `echo "The quick"; echo "brown fox";`
- If a command goes to a pager (ie it scrolls instead of printing out normally) you can try piping it into `cat` e.g. `man git | cat`

## Script as a Function

This is *exactly* the same as **Script as a String**, except, as you may have guessed, you can define what script to run as a **Function** as opposed to a **String.**

```jsx
args: {

		// Take an array of what the user has already input
		// e.g. 
		script: function (context: Array<string>) { 
					
				var myScript; 
				
				if (contextArray
							
				// Return string
				return myScript
		},

		splitOn: "",
		// **OR**
		postProcess: (scriptOutput: string) => {			
		},

		
		// [optional]
		trigger: (after: string, before: string) {
		}
}
```

The properties below are exactly the same as **Script as a String** except for the `script` prop. In that case

Properties

| Property    | Data Type                                                    | Description                                                  |
| ----------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| script      | function(context: array): string { }<br /><br /> **Input**: output of executing script <br />**Output**: array of Suggestion objects | The shell command to execute in the user's current working directory. The output is a string. It is then converted into an array of Suggestion objects using `splitOn` or `postProcess`<br /><br /> e.g. git branch → show all the remote git repos available |
| postProcess |                                                              | See [postProcess above]()                                    |
| splitOn     |                                                              | See [splitOn above]()                                        |
| trigger     | function or string                                           | **[Optional]** See [Trigger]()                               |
| filterTerm  | function or string                                           | **[Optional]** See [Filter Term]()                           |

## Custom Function

The **Script as a String** or **Script as a Function** generator functions above should suit your needs needs most of the time. By using a custom function, we anticipate you may be overcomplicating things. In fact, we suggest doing a very simple version of the spec you want to write using the generators first. It may not capture every single use case, but if it's > 60% or 70% of the use cases, worst case, Fig just won't show for the remaining use cases. You can also run a string that is multiple commands e.g. `echo "The quick"; echo "brown fox";` to get multiple outputs in one go. Once that's working, then try a Custom Function.

If you have read everything and really think you know what you're doing, then please dig in :). In fact, if you are going to write a Custom Function, please email us, we'd love to help

[hello@withfig.com](mailto:hello@withfig.com)

Fig's completion spec standard account for (what we hope) is the vast majority of CLI tools with just the functions you have already seen. However, inevitably, CLI tools grow in ability and some of their features don't work with the standard spec. Custom Functions inside generators should enable you to solve for this and do way way more.

Custom Functions let you define a function that takes an array of what the user has typed, run as many shell commands as you'd like on the user's machine, and then generate suggestions to display. When using Custom Functions, you will likely have to work pretty closely with [Triggers](#trigger).

Custom functions are so customisable, you could theoretically add one to an arg of your root command and build your own autocomplete server, all in javascript - it would be one big function! (but let's not get carried away)

Before we get into the syntax, let's look at where we would use one of these.

### When to use Custom Functions

**1. An argument can be one of many things and you want to provide suggestions once you have worked out which "thing"  the user is typing.** e.g. in `git` you can identify a commit in many many ways.

- `git checkout staging` → branch
- `git checkout h8ne3x` → commit hash
- `git checkout HEAD~` → Relative refspec

(If you're interested [here are a lot more](https://stackoverflow.com/a/18605496/2218728) )

You could just use a **script as a string** Generator and only suggest branches by using `git branch`. This would be nice and would work fine. But it would be cool if you could type `HEAD^^` and have Fig tell you which commit description you are referring to... Custom functions let you do this.

**2. An argument takes its own sub-arguments that are not delimited by a space** e.g. in `npm` you can refer to a package in many ways AND then you can provide sub-arguments like the version, tag, and range, all within the same string

![](../assets/autocomplete/generators/subargs.png)

Your function could do multiple regex matches on the argument the user is inputting. If it begins with an `@` symbol, then suggest a list of scopes. As soon as the user types a `/` suggest a list of packages. As soon as the user types another `@` symbol, suggest a list of tags or versions associate with the input package name...

### Syntax

```jsx
args: {  
	generator: {

			custom: async function generateSuggestions(context: Array<string>): SuggestionObject {
			
					var currentArg = context[-1]
					var out;
		
					if (currentArg.includes(":")) {
							out = await runFigCommand("foo")
					}
					else {
							out = await runFigCommand("bar")
					}
					
					return out.split("\\n") 
			},

			trigger: SEE BELOW,
			filterTerm: SEE BELOW
	}	
}
```

# Trigger

Trigger when we should recall the generators for this argument.

e.g. when you use "cd" in Fig, we set a trigger for "/"

- can be a string:
  - e.g. if trigger: "/", re-run the generators every time the last index of "/" is different between the previous input and the current input
- can be a function

```bash
fn(currentString: str, previousString: str): bool { }

e.g. fn("desk", "Desktop/") if fn was:

fn function (curr,prev) {

	if (curr.lastIndexOf("/") !== prev.lastIndexOf("/")) return true
	else return false

})
```

# Filter Term

A function to determine what part of a string the user is currently typgin we should use to filter our suggestions.

The default is the same string

```jsx
filterTerm: (currentString: string): string => {

}
```

When would you want to use this?

e.g. in `cd` the user may have typed `~/Desktop/b`

- Our trigger function told us to regenerate suggestions as soon as we saw a new forward slash
- Our suggestions show all the folders in the `~/Desktop` directory
- But as the user types, Fig defaults to filter over the suggestions using `~/Desktop/b` as the search term. We only want the search term to be `"b"`

Here is the function we would write:

```java
filterTerm: (curr) => {

	if curr.includes("/") {
		return curr.slice(curr.lastIndexOf("/") + 1)	
	}

	else return curr

}
```

Because this use case may be common, we have also defined a string that makes this simpler

```jsx
filterTerm: "/"
```

We take the user input string, and take everything to the right of the filterTerm property defined, if it's present

Finally, if you have multiple generators, Fig will only take into account the very last filterTerm function or string you define.

the filterTerm fig uses under the hood for file and folder templates is exactly the same as the one in the example just above. Therefore, if you want do use multiple generators for an argument, and one of the generators is template suggestions, you should make sure you include the template generator first in the generators array and to define your filterTerm function thereafter (and ideally for it to take into account the forward slashes...).