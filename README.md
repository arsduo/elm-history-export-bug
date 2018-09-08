## Elm History Export Bug

For some reason, this minimal setup for a counter program is experiencing a bug with Elm's debug
history exports. Compiled with either elm-make or with webpack, clicking the counter buttons a few
times and then exporting the history yields malform data like so:

```json
{"$":0,"a":{"metadata":{"versions":{"elm":"0.19.0"},"types":{"message":"Main.Msg","aliases":{},"unions":{"Main.Msg":{"args":[],"tags":{"Decrement":[],"Increment":[],"UpdateSecretField":["String.String"]}},"String.String":{"args":[],"tags":{"String":[]}}}}},"history":[null,null,null,null,null]}}
```

The export works fine for @rtfeldman's [Elm SPA
example](https://github.com/rtfeldman/elm-spa-example/), so it must be something subtle about this
code, but for the life of me I can't figure it out.

**Expected:** the history field contains data about the messages that have been received

**Actual:** each entry is null.

**Steps to reproduce:**

1. Install Elm/etc. by running `yarn install` (or npm if you want)
2. `yarn run elm make --debug --output index.html Main.elm`
3. `open index.html` in whatever browser you want
4. Click some buttons
5. Export history and view the resulting JSON data

You can also test this against webpack:

1. Install Elm as above
2. Run `yarn server`
3. Trigger actions and view the history data as above


