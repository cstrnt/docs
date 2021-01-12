#  Autocomplete for your Internal CLI

Everything works exactly the same as in the previous docs.

We suggest creating a symlink of your completion spec doc from a git versioned repo to the `~/.fig/autocomplete` folder

e.g. if your company's git versioned monorepo is called `monorepo` and your internal cli tool is called `acme`, do the following:

```bash
# This is the format for doing a symbolic link
ln -s /path/to/original /path/to/link

ln -s ~/monorepo/acme.js ~/.fig/autocomplete/acme.js
```

Remember, your completion spec file name must be the same as your internal cli tool name (e.g. `acme` → `acme.js`)