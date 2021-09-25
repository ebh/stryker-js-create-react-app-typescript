# StrykerJS with create-react-app (TypeScript)

This repo exists assist in raising a ticket for [stryker-mutator/stryker-js](https://github.com/stryker-mutator/stryker-js).

This branch reflects running the process documented by [Getting started](https://stryker-mutator.io/docs/stryker-js/getting-started) only.


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

### Install StrykerJS

Run:
```
stryker init
```

Answer to questions:
| Questions                                                                    | Answer           |
| ---------------------------------------------------------------------------- | ---------------- |
| Do you want to install Stryker locally?                                      |  yarn            |
| Are you using one of these frameworks? Then select a preset configuration.   | create-react-app |
| What file type do you want for your config file?                             | JSON             |
| Which package manager do you want to use?                                    | yarn             |


### Run Stryker

```
stryker run
```

## Expected Result

* Some kind of failure, because I had not performed the [TypeScript Checker](https://stryker-mutator.io/docs/stryker-js/typescript-checker) process

## Actual Results

* It seems to work, as I see this:

```
15:26:58 (47621) INFO ConfigReader Using stryker.conf.json
15:26:58 (47621) INFO InputFileResolver Found 5 of 32 file(s) to be mutated.
15:26:59 (47621) INFO Instrumenter Instrumented 5 source file(s) with 9 mutant(s)
15:26:59 (47621) INFO ConcurrencyTokenProvider Creating 7 test runner process(es).
15:27:01 (47621) INFO DryRunExecutor Starting initial test run (jest test runner with "off" coverage analysis). This may take a while.
15:27:04 (47621) INFO DryRunExecutor Initial test run succeeded. Ran 1 tests in 3 seconds (net 38 ms, overhead 3108 ms).
Mutation testing  [==================================================] 100% (elapsed: <1m, remaining: n/a) 9/9 tested (8 survived, 0 timed out)

All tests/App.test.tsx
  ✓ renders learn react link [line 5] (killed 1)

#1. [Survived] StringLiteral
src/index.tsx:11:27
-     document.getElementById('root')
+     document.getElementById("")
Ran all tests for this mutant.

#3. [Survived] ConditionalExpression
src/reportWebVitals.ts:4:7
-     if (onPerfEntry && onPerfEntry instanceof Function) {
+     if (true) {
Ran all tests for this mutant.

#4. [Survived] ConditionalExpression
src/reportWebVitals.ts:4:7
-     if (onPerfEntry && onPerfEntry instanceof Function) {
+     if (false) {
Ran all tests for this mutant.

#5. [Survived] LogicalOperator
src/reportWebVitals.ts:4:7
-     if (onPerfEntry && onPerfEntry instanceof Function) {
+     if (onPerfEntry || onPerfEntry instanceof Function) {
Ran all tests for this mutant.

#2. [Survived] BlockStatement
src/reportWebVitals.ts:3:58
-   const reportWebVitals = (onPerfEntry?: ReportHandler) => {
-     if (onPerfEntry && onPerfEntry instanceof Function) {
-       import('web-vitals').then(({ getCLS, getFID, getFCP, getLCP, getTTFB }) => {
-         getCLS(onPerfEntry);
-         getFID(onPerfEntry);
-         getFCP(onPerfEntry);
-         getLCP(onPerfEntry);
-         getTTFB(onPerfEntry);
-       });
-     }
-   };
+   const reportWebVitals = (onPerfEntry?: ReportHandler) => {};
Ran all tests for this mutant.

#7. [Survived] StringLiteral
src/reportWebVitals.ts:5:12
-       import('web-vitals').then(({ getCLS, getFID, getFCP, getLCP, getTTFB }) => {
+       import("").then(({ getCLS, getFID, getFCP, getLCP, getTTFB }) => {
Ran all tests for this mutant.

#8. [Survived] BlockStatement
src/reportWebVitals.ts:5:80
-       import('web-vitals').then(({ getCLS, getFID, getFCP, getLCP, getTTFB }) => {
-         getCLS(onPerfEntry);
-         getFID(onPerfEntry);
-         getFCP(onPerfEntry);
-         getLCP(onPerfEntry);
-         getTTFB(onPerfEntry);
-       });
+       import('web-vitals').then(({ getCLS, getFID, getFCP, getLCP, getTTFB }) => {});
Ran all tests for this mutant.

#6. [Survived] BlockStatement
src/reportWebVitals.ts:4:55
-     if (onPerfEntry && onPerfEntry instanceof Function) {
-       import('web-vitals').then(({ getCLS, getFID, getFCP, getLCP, getTTFB }) => {
-         getCLS(onPerfEntry);
-         getFID(onPerfEntry);
-         getFCP(onPerfEntry);
-         getLCP(onPerfEntry);
-         getTTFB(onPerfEntry);
-       });
-     }
+     if (onPerfEntry && onPerfEntry instanceof Function) {}
Ran all tests for this mutant.

Ran 0.11 tests per mutant on average.
--------------------|---------|----------|-----------|------------|----------|---------|
File                | % score | # killed | # timeout | # survived | # no cov | # error |
--------------------|---------|----------|-----------|------------|----------|---------|
All files           |   11.11 |        1 |         0 |          8 |        0 |       0 |
 App.tsx            |  100.00 |        1 |         0 |          0 |        0 |       0 |
 index.tsx          |    0.00 |        0 |         0 |          1 |        0 |       0 |
 reportWebVitals.ts |    0.00 |        0 |         0 |          7 |        0 |       0 |
--------------------|---------|----------|-----------|------------|----------|---------|
15:27:05 (47621) INFO HtmlReporter Your report can be found at: file:///Users/ebh/git/github/ebh/stryker-js-create-react-app-typescript/reports/mutation/html/index.html
15:27:05 (47621) INFO MutationTestExecutor Done in 6 seconds.
```

## Stryker Version

Running `stryker --version` returns `5.4.0`
