# How to write a test

Tests are contained in the directory `test` of the Jolie repository.

## How to run tests

Tests can be run either by issuing the command `ant test` or by going inside of the `test` subdirectory and running `jolie test.ol`. The test program accepts regular expressions as a parameter, in case you want to run only a few selected tests. For example, to run only tests whose names contain the string `expressions`, you can run the command `jolie test.ol ".*expressions.*"`.

## To create a new test

Create a new Jolie program inside of one of the subdirectories of `test`. To start with, you can simply copy the `test_template.ol` file and rename it appropriately. The file contains instructions on how to write the test.

You must place your test program inside of a subdirectory of `test`. There are already a few subdirectories, for example:

* `primitives` contains tests for language constructs;
* `extensions` contains tests for extensions, like `http` and `sodep`;
* `library` contains tests for the Jolie Standard Library \(e.g., Java services\).

The Jolie test program \(`test.ol`\) runs only tests that are placed inside of a first-level subdirectory of the `test` directory. Nested directories inside of those \(for example, directories inside of `primitives`\) are not explored. This is useful in case you need to store auxiliary files needed by a test. It happens often when the test consists of multiple services, for example see the test `extensions/http_get.ol`.

