# How to make a pull request

A pull request should be minimal. Ideally, it should either fix one bug or add a new feature. This is what we should strive for, but of course there are exceptions. For example, sometimes a minimal code modification fixes a bug _and_ introduces a feature.

In any case, the general rule of thumb is that big pull requests are a bad idea \(big in the sense that there are a lot of changes, or that there is a lot of new code\). The smaller the pull request, the better, and the more likely that it will be processed in a reasonable time. Make a big pull request with no good reason, and forever may it linger in the limbo of forgotten pull requests.

A pull request should thus:

* be minimal, as described above;
* if it fixes a bug that was not caught by the test suite, it should include a test such that we can detect this bug in the future \(see [how to write a test](https://github.com/jolielang/developer-guide/tree/b5749ca31c05ed4e803574d335aefd2cc0be944e/tests.html)\);
* if it introduces a feature, it should include tests for the new feature \(see [how to write a test](https://github.com/jolielang/developer-guide/tree/b5749ca31c05ed4e803574d335aefd2cc0be944e/tests.html)\).

