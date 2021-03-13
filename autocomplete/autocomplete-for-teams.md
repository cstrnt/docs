#  Autocomplete for your Teams

Fig allows teams to build autocomplete for their internal CLIs and scripts. A "team" is anyone logged in to Fig with the same email domain as you

To invite your team mates to Fig, get your personal referral link by running `fig invite`

## Internal CLI

Let's say your company has an internal CLI called `acme`. 

You can build a completion spec for your CLI tool and upload it to Fig's cloud.

```bash
fig team:upload </path/to/completion_spec.js>
```

Now you can tell your team members with Fig installed to download the spec you just pushed. Every time an update it pushed, team members can run the same command.

```bash
fig team:download
```

Under the hood, we are saving the spec to Fig's cloud namespaced by your domain name. Then when user's download it, we save it in the `~/.fig/teams/autocomplete` folder and symlink it to their `~/.fig/autocomplete` folder.


## Internal Scripts

Let's say you are working in a git repo with a script folder. That folder contains executables like `deploy.sh` or other scripts like `tests.py` or `build.js`. Let's say these scripts each take different arguments, subcommands, and flags. You would like to build autocomplete for them to make it easy for your team.

In the same directory as your scripts, you may include a `.fig/` folder which contains completion specs for each of these scripts. These completion specs are the same format as documented everywhere else. Importantly, they must be named `<script name and file extension>.js`

e.g. `.fig/deploy.sh.js` `.fig/tests.py.js` or `.fig/build.js.js`

Now, when you run a script like `./deploy.sh` or `python main.py` or `node build.js` Fig will start autocompleting on the arguments for the given script. 

You can version control your completion specs with your scripts in your git repo.

