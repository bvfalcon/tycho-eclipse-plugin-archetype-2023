tycho-eclipse-plugin-archetype
==============================

This archetype will create a multi-module project with a nested structure :

     __artifactId__    : parent pom project
     |
     |---__artifactId__.core   : eclipse-plugin
     |
     |---__artifactId__.feature: eclipse-feature
     |
     |---__artifactId__.test   : eclipse-test-plugin (Fragment project)
     |
     |---__artifactId__.site : eclipse-repository

The generated plugin is based on the Hello World template from the PDE Wizard, using the Eclipse 3.x architecture :

    [...] creates a simple handler set that adds Sample Menu to the menu bar and a button to the tool bar.
    Both the menu item in the new menu and the button invoke the same Sample Handler.
    Its role is to open a simple message dialog with a message of your choice.

Pre-Requisites :
-------------------

* JDK 1.8 or later (Java 17 is the default target)
* Maven 3.6.3 or later
* Eclipse 2022-12 is the default target, but earlier versions *might* work
* m2e 1.1 or later
* m2eclipse-tycho 0.6 or later

Accessing the archetype from Eclipse
-------------------
In Eclipse, first add the Open Archetypes catalog :

1. On the Archetypes Preferences page (Windows: `Window` > `Preferences`; OS X: `Eclipse`> `Preferences` or `⌘,`), open `Maven` > `Archetypes`, click on the `Add Remote Catalog...` button

    - Catalog file : https://s3.eu-central-1.amazonaws.com/github.bvfalcon/maven-repo/
    - Description : `Open Archetypes`

2. Click `OK` to close the dialog
3. Click `OK` to close the preferences
 
Accessing the archetype from command line
-------------------
Open your terminal or Windows CMD:

1. Execute `mvn org.apache.maven.plugins:maven-archetype-plugin:2.4:generate -DarchetypeCatalog=https://s3.eu-central-1.amazonaws.com/github.bvfalcon/maven-repo/ -DarchetypeGroupId=org.openarchetypes -DarchetypeArtifactId=tycho-eclipse-plugin-archetype`
2. Enter the groupId
3. Enter the artifactId
4. Enter the name of the package under which your code will be created
5. Enter the version of your project
6. Confirm

Creating a new project in Eclipse, using the Maven wizard
-------------------

1. Create a new Maven project
* Click `Next` to land on the Archetype page
* Select the `Open Archetypes` catalog
* Select `tycho-eclipse-plugin-archetype` and click Next
* Enter the Group Id, Artifact Id and Version informations. Eclipse requires the version to follow a Major.Minor.Micro pattern, so you should use 1.0.0-SNAPSHOT instead of 1.0-SNAPSHOT
* You can change the required properties if needed :
    - java_version : The Java version to be used for compiling the plugins. Supported values are `1.8` to `17`. Defaults to `17`
    - tycho_version : the tycho version that will be used to build the project in command line. Defaults to `3.0.1`
    - eclipse_platform : the Eclipse platform, will drive what eclipse update site will be used to resolve the Eclipse dependencies. Defaults to `2022-12`. Previous non-date-based platforms like `neon`, `luna` might work too.
* Hit `Finish`
* Wait for awesomeness

Once the projects are created, you can start testing Eclipse hosted mode, run JUnit Plug-in tests ...

Building the project with Maven
-------------------
You can then build your projects in command line, in a terminal, by issuing :

    mvn clean verify

A zipped update site will be created as `<project.parent>/<project.site>/target/<project.site>-<project.version>-site.zip`.

Signed artifacts
-------------------
Signing artifacts with PGP signature is possible with profile `sign`.

    mvn package -Psign


Alternative archetypes
----------------------
You can find somewhat similar tycho-based archetypes based on :

* Groovy : https://github.com/open-archetypes/groovy-eclipse-plugin-archetype
* XText : https://github.com/fuinorg/emt-xtext-archetype
