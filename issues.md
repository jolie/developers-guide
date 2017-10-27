# How to post a bug issue

A bug issue must contain:
* The version of the Jolie interpreter;
* identifier of the operating system;
* the stack trace printed by the interpreter, if available;
* a link to a pull request that tests the bug.

The next section gives an example of how to proceed correctly with the creation of the pull request and the issue.

## Development process

1. You have found a bug. Congratulations!
2. Think carefully: is it a bug in your code, or is it a bug in the interpreter?
3. If you believe that the bug is in the interpreter, continue.
4. Open a new branch in your working Jolie git repository. Example: `git checkout -b issue-42`. Be careful: you should use this branch _only_ for working on this issue, not other issues. Also, be sure that you are creating the branch starting from the `master` branch (which should be in sync with the upstream repository).
5. [Write a test](tests.html). The test should be minimal (it tests only the issue) and it should fail because of the bug that you have found.
6. Issue a pull request to the [upstream Jolie git repository](https://github.com/jolie/jolie) with the test.
7. [Open an issue](https://github.com/jolie/jolie/issues) with a link to the pull request containing the test (e.g., if the pull request number is `42`, you can write `#42` in the issue comments).
