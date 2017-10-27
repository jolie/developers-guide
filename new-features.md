# Process (tentative) for keeping track of discussions on new features

1. Open discussion. Suggestion to start it: use the `jolie-devel@googlegroups.com` mailing list.
2. A new repository on [jolie-projects](https://github.com/jolie-projects) is created for discussing the proposal.
3. Examples are produced in pseudo-code that describe what we want to be able to do.
4. Discussion continues on GitHub (in-code comments) or other media (e-mail, shared documents, etc.). However, _code is always put on the git repository_!
5. [Tests are produced](tests.html), which capture what the new features should do, and a general description of the new features that is as concise as possible is put on the `README.md` of the git repository.
6. Work commences on a separate branch of the Jolie git repository to develop the new feature. In alternative, if the feature is already being developed in some other repository, a pull request is issued to the Jolie repository once completed.
