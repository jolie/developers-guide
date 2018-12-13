# Debugging Jolie in Netbeans

Sometimes it is useful to debug the execution of a Jolie program from Netbeans. The following is an example of how to do that on Linux, assuming that:

* Jolie is installed in `/opt/jolie` ;
* the path to the Jolie program to run is `main.ol`;
* the path to the directory of the Jolie program to run is `/path/to/your/jolie_service/`.

Run -&gt; Set Main Project -&gt; jolie

Run -&gt; Set Project Configuration -&gt; Customize

* Main Class: `jolie.Jolie`
* Arguments: `-l /opt/jolie/lib:/opt/jolie/javaServices/*:/opt/jolie/extensions/* -i /opt/jolie/include main.ol`
* Working Directory: `/path/to/your/jolie_service/`

## Debugging Jolie modules \(extensions\)

When debugging a package \(usually correspondent to a Netbeans project\) within the Jolie repository , it can be useful \(e.g., quicker/easier testing\) to compile it in a `.jar` from Netbeans and make the Jolie interpreter use that `.jar`. To do so, we need to make sure of two things: that we compiled the extension via Netbeans and that we are loading the Netbeans-compiled version of the extension in the Run command.

To understand how to do those steps, let us consider the case of a Jolie extension \(found under the directory `extensions` under the root of the Jolie repository\). The procedure holds also to any package within the Jolie repository.

In our example, let us consider a module called `my-extension` which generates a file `my-extension.jar` ; the project is located under directory `extensions` .

### Running Jolie with the correct .jar package

Now, let us first make sure that our Run command executes Jolie with our Netbeans-compiled extension. First we must remove any pre-existing `my-extension.jar` in the `extensions` directory where the `jolie.jar` resides; considering the path above, `/opt/jolie`, we need to look into `/opt/jolie/extensions` and remove any file called `my-extension.jar` present there.

Finally we can instruct the Run configuration to source the Netbeans-compiled `.jar`. Let us consider `/Users/username/projects/jolie/extensions/my-extension` the absolute path \(but also relative paths are allowed\) where our extension is located. All we have to do is to include the string `/Users/username/projects/jolie/extensions/my-extension/dist/*` within the Arguments Run properties, such that `-l /opt/jolie/lib:/opt/jolie/javaServices/*:/opt/jolie/extensions/* -i /opt/jolie/include main.ol` from above becomes

`-l /opt/jolie/lib:/opt/jolie/javaServices/*:/opt/jolie/extensions/*:/Users/username/projects/jolie/extensions/my-extension/dist/* -i /opt/jolie/include main.ol`.

### Compiling the .jar

Once configured the Run command, we can compile our extension via Netbeans. To do this we just need to click on the Build button, which should create a `.jar` under the directory `jolie_repo/extensions/my-extension/dist/` . Done that, we can proceed and Run our configuration, which should source the newly compiled `.jar` file. From now on we can modify, re-compile, and test the sources of the package directly from Netbeans.

