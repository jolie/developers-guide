# Code style

These are some general rules to follow when editing the Java code of the Jolie project.  
To see the precise spacing that we use, the best way is just to have a look at the existing code.  
If you use NetBeans and are in doubt or just lazy, at the very least use  
[Fabrizio's NetBeans formatting settings](/files/netbeans_formatting.zip) \(you can import them from the preference panel in NetBeans\) and run the `Source -> Format` command before committing.

## The Rules

* Use tabs for indentation, not spaces. Some editors expand tabs into spaces automatically: make sure that you are not doing it.
* If you want to restyle some code, _always_ make it a separate commit or pull request. _Never_ make a pull request where you change the style of existing code _and_ change code at the same time, or the difference will become very hard to see using automatic tools.
* Try to keep methods as short as possible. Split them in multiple private methods if necessary.
* Use lowercaseCamelCase for variable and method names and UppercaseCamelCase for class names.
* For getter and setters: use the same name of the property for getter methods, e.g., `public String name()` \(_not_ `getName()`!\), and use the `set` prefix for setter methods, e.g., `public void setName( String name )`.



