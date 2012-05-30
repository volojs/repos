# volojs/repos

A set of package.json and amd.json files that serve as "overrides" for github repos that do not have the correct information in the repos themselves.

## package.json

`volo add` will look for a ["volo" property in a package.json]() to find a download location for any project that does not follow the default conventions used by volo to find the installable piece of code.

If a project does not have a "volo" property in their package.json for the latest version tag of their project, then this repo is consulted for an override.

See the [package.json info]() on the volo wiki for what kinds of volo information can go in a package.json.

## amd.json

For projects that specify an "amd" section in their package.json, `volo add` will attempt to convert a dependency to be an AMD module wrapped in a `define()` call. `volo add` scans the file, and if it is already calling `define()` then it will do nothing.

However if the file does not call define, `volo add` will reach out to this repo and look for a `user/repo/amd.json` file that specifies the dependencies and exports for the file and use that to wrap the file.

If there is no amd.json file in this repo, then the user is prompted for the answers.

This can be turned off for a particular add by passing -amdoff to the add command: `volo add -amdoff`.

An example amd.json for Backbone:

```json
{
    "deps": ["jquery", "underscore"],
    "exports": "Backbone"
}
```

If there are no dependencies, you can pass an empty array. Example one for Zepto:

```json
{
    "deps": [],
    "exports": "Zepto"
}
```
