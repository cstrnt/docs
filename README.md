# Fig Docs

This repo hosts all of Fig's docs, found at [withfig.com/docs](https://withfig.com/docs).

To make changes to a doc, fork this repo and submit a PR.

### Adding a new doc

Under the docs folder, you'll find a bunch of markdown files, with even more markdown files inside some nested folders. These files represent each doc's contents and their URL path. For example, if you wanted to add something under the Autocomplete section of the sidebar, make sure to add that markdown file under the /autocomplete folder. Files under the /autocomplete folder will also be routed under withfig.com/docs/autocomplete.

After moving the .md file into the right /docs path, we need to set up URL routing to your doc. Routing is handled by the `manifest.json` file found under /docs. This file also determines the order that the docs will show up on the sidebar.

**Additional properties**

- To create a hidden page, one that can be accessed via URL but can't be found in the sidebar (ex: [https://withfig.com/docs/support/secure-keyboard-input](https://withfig.com/docs/support/secure-keyboard-input)), add `"show": false`.

```js
{
    "title": "Secure Keyboard Input",
    "path": "support/secure-keyboard-input.md",
    "show": false
}
```

### Updating a doc

You can make changes to any of the docs by directly editing the .md files in the /docs folder. To change the order that docs show up on the sidebar, rearrange the manifest.json accordingly.