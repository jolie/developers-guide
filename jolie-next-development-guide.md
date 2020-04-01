# \[Orphan?\] Jolie Test Suite with new classloader

### Running the Jolie Test Suite with the new JolieClassLoader

Arguments:

```text
-l  ../dist/jolie/lib:../javaServices/*/dist/*:../extensions/*/dist/* -i /Users/thesave/projects/jolie_next/dist/jolie/include test.ol
```

Note that the loader now can expand in-path wildcards, so that, e.g., `extensions/*` captures all the subfolders of inside the `extensions` folder \(e.g., http, https, etc.\). This removes the need to run `ant`  to run the tests, as it just requires a build performed from Netbeans.

Working Directory:

```text
path/to/jolie_git_repo/test
```

VM Options:

```text
-ea:jolie... -ea:joliex... -Djava.rmi.server.codebase=file:/../dist/jolie/extensions/rmi.jar
```

