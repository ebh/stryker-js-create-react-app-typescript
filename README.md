# StrykerJS with create-react-app (TypeScript)

This repo exists assist in raising a ticket [stryker-mutator/stryker-js](https://github.com/stryker-mutator/stryker-js).

This branch reflects running the process documented by [StrykerJs->Guides->React](https://stryker-mutator.io/docs/stryker-js/guides/react/).


## Steps to Reproduce

### Create fresh create-react-app App (TypeScript)

Run:
```
npx create-react-app stryker-js-create-react-app-typescript --template typescript
cd stryker-js-create-react-app-typescript
```

### Verify tests are working

Run:
```
CI=true yarn test
```

You should see:
```
yarn run v1.22.11
$ react-scripts test
PASS src/App.test.tsx
  ✓ renders learn react link (26 ms)

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        1.228 s
Ran all test suites.
✨  Done in 2.06s.
```

### Add StrykerJS

Run:
```
yarn add -D @stryker-mutator/core @stryker-mutator/jest-runner @stryker-mutator/typescript @stryker-mutator/html-reporter
```

### Create config

`stryker.conf.js`:
```
module.exports = function (config) {
  config.set({
    mutate: ['src/**/*.ts?(x)', '!src/**/*@(.test|.spec|Spec).ts?(x)'],
    mutator: 'typescript',
    testRunner: 'jest',
    reporter: ['progress', 'clear-text', 'html'],
    coverageAnalysis: 'off',
    jest: {
      project: 'react',
    },
  });
};
```

### Run Stryker

```
stryker run
```

## Expected Result

* Stryker to output mutation report

## Actual Results

```
15:09:43 (46559) INFO ConfigReader Using stryker.conf.js
15:09:43 (46559) WARN ConfigReader Usage of `module.exports = function(config) {}` is deprecated. Please use `module.export = {}` or a "stryker.conf.json" file. For more details, see https://stryker-mutator.io/blog/2020-03-11/stryker-version-3#new-config-format
The @stryker-mutator/html-reporter package is a stub package. The html reporter is now included with @stryker-mutator/core. There is no need to have the @stryker-mutator/html-reporter package installed! Are you still using stryker v2? Then please upgrade stryker to at least 3.x using or downgrade this plugin to the latest 2.x release.
The @stryker-mutator/typescript package does not have any function in Stryker 4.0. Please remove it from your devDependencies.
15:09:44 (46559) WARN OptionsValidator DEPRECATED. Use of "mutator" as string is no longer needed. You can remove it from your configuration. Stryker now supports mutating of JavaScript and friend files out of the box.
15:09:44 (46559) ERROR OptionsValidator Config option "jest" must NOT have additional properties
15:09:44 (46559) ERROR Stryker Please correct this configuration error and try again.
```

## Stryker Version

Running `stryker --version` returns `5.4.0`
