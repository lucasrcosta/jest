---
id: version-23.2-cli
title: Jest CLI Options
original_id: cli
---

The `jest` command line runner has a number of useful options. You can run `jest --help` to view all available options. Many of the options shown below can also be used together to run tests exactly the way you want. Every one of Jest's [Configuration](Configuration.md) options can also be specified through the CLI.

Here is a brief overview:

## Running from the command line

Run all tests (default):

```bash
jest
```

Run only the tests that were specified with a pattern or filename:

```bash
jest my-test #or
jest path/to/my-test.js
```

Run tests related to changed files based on hg/git (uncommitted files):

```bash
jest -o
```

Run tests related to `path/to/fileA.js` and `path/to/fileB.js`:

```bash
jest --findRelatedTests path/to/fileA.js path/to/fileB.js
```

Run tests that match this spec name (match against the name in `describe` or `test`, basically).

```bash
jest -t name-of-spec
```

Run watch mode:

```bash
jest --watch #runs jest -o by default
jest --watchAll #runs all tests
```

Watch mode also enables to specify the name or path to a file to focus on a specific set of tests.

## Using with yarn

If you run Jest via `yarn test`, you can pass the command line arguments directly as Jest arguments.

Instead of:

```bash
jest -u -t="ColorPicker"
```

you can use:

```bash
yarn test -u -t="ColorPicker"
```

## Using with npm scripts

If you run Jest via `npm test`, you can still use the command line arguments by inserting a `--` between `npm test` and the Jest arguments.

Instead of:

```bash
jest -u -t="ColorPicker"
```

you can use:

```bash
npm test -- -u -t="ColorPicker"
```

## Options

_Note: CLI options take precedence over values from the [Configuration](Configuration.md)._

<AUTOGENERATED_TABLE_OF_CONTENTS>

---

## Reference

### `jest <regexForTestFiles>`

When you run `jest` with an argument, that argument is treated as a regular expression to match against files in your project. It is possible to run test suites by providing a pattern. Only the files that the pattern matches will be picked up and executed. Depending on your terminal, you may need to quote this argument: `jest "my.*(complex)?pattern"`. On Windows, you will need to use `/` as a path separator or escape `\` as `\\`.

### `--bail`

Alias: `-b`. Exit the test suite immediately upon the first failing test suite.

### `--cache`

Whether to use the cache. Defaults to true. Disable the cache using `--no-cache`. _Note: the cache should only be disabled if you are experiencing caching related problems. On average, disabling the cache makes Jest at least two times slower._

If you want to inspect the cache, use `--showConfig` and look at the `cacheDirectory` value. If you need to clear the cache, use `--clearCache`.

### `--changedFilesWithAncestor`

Runs tests related to the current changes and the changes made in the last commit. Behaves similarly to `--onlyChanged`.

### `--changedSince`

Runs tests related the changes since the provided branch. If the current branch has diverged from the given branch, then only changes made locally will be tested. Behaves similarly to `--onlyChanged`.

### `--ci`

When this option is provided, Jest will assume it is running in a CI environment. This changes the behavior when a new snapshot is encountered. Instead of the regular behavior of storing a new snapshot automatically, it will fail the test and require Jest to be run with `--updateSnapshot`.

### `--clearCache`

Deletes the Jest cache directory and then exits without running tests. Will delete `cacheDirectory` if the option is passed, or Jest's default cache directory. The default cache directory can be found by calling `jest --showConfig`. _Note: clearing the cache will reduce performance._

### `--collectCoverageFrom=<glob>`

A glob pattern relative to <rootDir> matching the files that coverage info needs to be collected from.

### `--colors`

Forces test results output highlighting even if stdout is not a TTY.

### `--config=<path>`

Alias: `-c`. The path to a Jest config file specifying how to find and execute tests. If no `rootDir` is set in the config, the directory containing the config file is assumed to be the rootDir for the project. This can also be a JSON-encoded value which Jest will use as configuration.

### `--coverage`

Indicates that test coverage information should be collected and reported in the output.

### `--debug`

Print debugging info about your Jest config.

### `--detectOpenHandles`

Attempt to collect and print open handles preventing Jest from exiting cleanly. Use this in cases where you need to use `--forceExit` in order for Jest to exit to potentially track down the reason. Implemented using [`async_hooks`](https://nodejs.org/api/async_hooks.html), so it only works in Node 8 and newer.

### `--env=<environment>`

The test environment used for all tests. This can point to any file or node module. Examples: `jsdom`, `node` or `path/to/my-environment.js`.

### `--errorOnDeprecated`

Make calling deprecated APIs throw helpful error messages. Useful for easing the upgrade process.

### `--expand`

Alias: `-e`. Use this flag to show full diffs and errors instead of a patch.

### `--findRelatedTests <spaceSeparatedListOfSourceFiles>`

Find and run the tests that cover a space separated list of source files that were passed in as arguments. Useful for pre-commit hook integration to run the minimal amount of tests necessary. Can be used together with `--coverage` to include a test coverage for the source files, no duplicate `--collectCoverageFrom` arguments needed.

### `--forceExit`

Force Jest to exit after all tests have completed running. This is useful when resources set up by test code cannot be adequately cleaned up. _Note: This feature is an escape-hatch. If Jest doesn't exit at the end of a test run, it means external resources are still being held on to or timers are still pending in your code. It is advised to tear down external resources after each test to make sure Jest can shut down cleanly. You can use `--detectOpenHandles` to help track it down._

### `--help`

Show the help information, similar to this page.

### `--init`

Generate a basic configuration file. Based on your project, Jest will ask you a few questions that will help to generate a `jest.config.js` file with a short description for each option.

### `--json`

Prints the test results in JSON. This mode will send all other test output and user messages to stderr.

### `--outputFile=<filename>`

Write test results to a file when the `--json` option is also specified.

### `--lastCommit`

Run all tests affected by file changes in the last commit made. Behaves similarly to `--onlyChanged`.

### `--listTests`

Lists all tests as JSON that Jest will run given the arguments, and exits. This can be used together with `--findRelatedTests` to know which tests Jest will run.

### `--logHeapUsage`

Logs the heap usage after every test. Useful to debug memory leaks. Use together with `--runInBand` and `--expose-gc` in node.

### `--maxWorkers=<num>`

Alias: `-w`. Specifies the maximum number of workers the worker-pool will spawn for running tests. This defaults to the number of the cores available on your machine. It may be useful to adjust this in resource limited environments like CIs but the default should be adequate for most use-cases.

### `--noStackTrace`

Disables stack trace in test results output.

### `--notify`

Activates notifications for test results. Good for when you don't want your consciousness to be able to focus on anything except JavaScript testing.

### `--onlyChanged`

Alias: `-o`. Attempts to identify which tests to run based on which files have changed in the current repository. Only works if you're running tests in a git/hg repository at the moment and requires a static dependency graph (ie. no dynamic requires).

### `--passWithNoTests`

Allows the test suite to pass when no files are found.

### `--projects <project1> ... <projectN>`

Run tests from one or more projects.

### `--runInBand`

Alias: `-i`. Run all tests serially in the current process, rather than creating a worker pool of child processes that run tests. This can be useful for debugging.

### `--runTestsByPath`

Run only the tests that were specified with their exact paths.

_Note: The default regex matching works fine on small runs, but becomes slow if provided with multiple patterns and/or against a lot of tests. This option replaces the regex matching logic and by that optimizes the time it takes Jest to filter specific test files_

### `--setupTestFrameworkScriptFile=<file>`

The path to a module that runs some code to configure or set up the testing framework before each test. Beware that files imported by the setup script will not be mocked during testing.

### `--showConfig`

Print your Jest config and then exits.

### `--silent`

Prevent tests from printing messages through the console.

### `--testNamePattern=<regex>`

Alias: `-t`. Run only tests with a name that matches the regex. For example, suppose you want to run only tests related to authorization which will have names like `"GET /api/posts with auth"`, then you can use `jest -t=auth`.

_Note: The regex is matched against the full name, which is a combination of the test name and all its surrounding describe blocks._

### `--testLocationInResults`

Adds a `location` field to test results. Useful if you want to report the location of a test in a reporter.

Note that `column` is 0-indexed while `line` is not.

```json
{
  "column": 4,
  "line": 5
}
```

### `--testPathPattern=<regex>`

A regexp pattern string that is matched against all tests paths before executing the test. On Windows, you will need to use `/` as a path separator or escape `\` as `\\`.

### `--testRunner=<path>`

Lets you specify a custom test runner.

### `--updateSnapshot`

Alias: `-u`. Use this flag to re-record every snapshot that fails during this test run. Can be used together with a test suite pattern or with `--testNamePattern` to re-record snapshots.

### `--useStderr`

Divert all output to stderr.

### `--verbose`

Display individual test results with the test suite hierarchy.

### `--version`

Alias: `-v`. Print the version and exit.

### `--watch`

Watch files for changes and rerun tests related to changed files. If you want to re-run all tests when a file has changed, use the `--watchAll` option instead.

### `--watchAll`

Watch files for changes and rerun all tests when something changes. If you want to re-run only the tests that depend on the changed files, use the `--watch` option.

### `--watchman`

Whether to use watchman for file crawling. Defaults to true. Disable using `--no-watchman`.