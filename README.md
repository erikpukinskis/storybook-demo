# Demonstration: Storybook not reading root .babelrc

There's a babel config in the root of this project, so it should be being read by Storybook. When I run `BABEL_SHOW_CONFIG_FOR=.storybook/preview.js npm run storybook` I would expect to see `@babel/preset-env` in the output.

But this is what I see instead:

```
Babel configs on "/Users/some_eriks/x/super-project-world/design-system/.storybook/preview.js" (ascending priority):
programmatic options from babel-loader
{
  "presets": [
    [
      "/Users/some_eriks/x/super-project-world/design-system/node_modules/babel-preset-react-app/index.js",
      {
        "runtime": "automatic"
      }
    ]
  ],
  "babelrc": false,
  "configFile": false,
  "plugins": [
    "/Users/some_eriks/x/super-project-world/design-system/node_modules/react-refresh/babel.js"
  ],
  "compact": false,
  "filename": "/Users/some_eriks/x/super-project-world/design-system/.storybook/preview.js",
  "sourceMaps": true,
  "sourceFileName": "/Users/some_eriks/x/super-project-world/design-system/.storybook/preview.js",
  "caller": {
    "name": "babel-loader",
    "target": "web",
    "supportsStaticESM": true,
    "supportsDynamicImport": true,
    "supportsTopLevelAwait": true
  }
}

programmatic options from babel-loader .overrides[0]
{
  "test": {},
  "plugins": [
    [
      "/Users/some_eriks/x/super-project-world/design-system/node_modules/babel-plugin-react-docgen/lib/index.js",
      {
        "DOC_GEN_COLLECTION_NAME": "STORYBOOK_REACT_CLASSES"
      }
    ]
  ]
}
-----End Babel configs-----
```

# Things I've tried that didn't work

* Using a `babel.config.js` file instead
* Using a `.babelrc.json` file instead
* Importing the `babel.config.js` inside `main.js`and manually splatting it together with the config provided

... None of those things have worked.

# Things I've tried that worked but don't exactly help

* Moving the `.babelrc` into `.storybook` _does_ work. But if I do that then I have to maintain two `.babelrc`, one for Storybook and one for the app and that doesn't seem quite right.
