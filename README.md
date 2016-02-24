# Introduction 
Our goal is to segregate the *CSS, FONT, HTML, and JS* *3rd party UI Libraries*, hereon referred to as *artifacts*, used to run the *application client*, hereon referred to as *iq_poc* from the *iq_poc*, while seamlessly:
* supporting the management of these *artifacts* during the *iq_poc* software construction process*.
* managing the *artifacts* during *maven builds*.
* maintaining version integrity.
 
## Elements
Our solution elements include:
 * *[Node](https://nodejs.org/en/)* - Node.js is a JavaScript runtime built on Chrome's V8 JavaScript engine. It is used to support the UI construction effort; it is not required to run the application. This document assumes the reader is thouroughly familar with [Node](https://nodejs.org/en/) and its modular architecture.
 * *[npm](https://www.npmjs.com/)* - the package manager for javascript.
 * *[linemanjs](http://linemanjs.com/)* - the development framework used to build the application UI.
 * *[bower](http://bower.io/)* - a package manager for the web.
 * *iq_poc/ngclient/src/main/webapp/node_modules* - the folder where the *node modules* are installed.
 * *iq_poc/ngclient/src/main/webapp/package.json* -  this file holds various *node module's* metadata relevant to the project.
 * *.gitignore*, a git file including a configuration to ignore the *iq_poc/ngclient/src/main/webapp/vendor* folder.
 * *[maven-exec](http://www.mojohaus.org/exec-maven-plugin/)*, a maven plugin used execute a build step to load the *artifacts*. 
 * *[lineman-maven-plugin](https://github.com/maxxkrakoa/lineman-maven-plugin/)*, a maven plugin used run *[linemanjs](http://linemanjs.com/)* scripts during the build. 

## Highlights
The collection of *artifacts* required to build *iq poc* is kept in the *ui_library* repository, separate from the *iq_poc* repository; it includes all *artifacts*, and their versions, ever used to build *iq_poc*; this is relevant to ensure support to build older *iq_poc* versions. The recipe to populate the *iq_poc* *UI Library folder*, *wepapps/vendor* and *webapps/spec*, with the required *artifacts* is kept in the *iq_poc* *webbapp/ui_library.json* file.

### the *UI Library* repository
* the *3rd party UI Library artifacts* are kept in the Github *ui_library* repository.
* each *UI Library* version is kept in its own folder
* each *UI Library* folder name is appended with its version.
* new *UI Libraries* are added as needed, using the folder naming scheme aforementioned.
 * old *UI Libraries* are never deleted, thus enabling us to build older versions of the application using older *UI Library* versions.
 
### the *ui_library.json* recipe
* describe the *UI Library* files required to build the *iq_poc* client
* is kept in the *iq poc* *webapps* folder.
* has one entry for each required *artifact*.
* is checked with the *iq_poc* changes.

### putting it all together
* the *iq_poc* client build:
  * navigates to the user's home folder
  * creates a *~/.dlabs* folder, if one does not exist.
  * clones the  *ui_library Github repository* in the *~/.dlabs folder*, if not already there.
    * **it is used by he build, do not do any work on it**.
  * checks out from *ui_library Github* repository, if *master* is not the current branch
  * pulls from *ui_library Github* repository
  * deletes the *webapps/vendor* and *webapps/spec* folders
  * populates the *webapps/vendor* and *webapps/spec* folder sby processing the *ui_library.json* file
 
## Workflow

### Development

### Add a new *UI Library*:
* clone the *ui_libraries Github repository* in your sandbox, if not already there; this is the user *ui_library local repository*; mine is on *~/Projects/ui_library*.
  * **DO NOT do so in the the *~/.dlabs folder***.
 * create a folder in your *ui_library local repository* to host the new *UI Library*; ensure to make it unique by using the new *UI Library's* version in the folder name.
 * populate the new *UI Library* folder.
   * most UI libraries can be retrieved using with *[bower](http://bower.io/)* or *[npm](https://www.npmjs.com/)*.
 * check in the changes to *ui_libraries local repository* into the *ui_libraries Github repository*.
 * update *webapp/ui_library.json* accordingly.
 * check in *webapp/ui_library.json*.
 * build the *iq_poc* client.

### Update an existing *UI Library*:
This amounts to replace an existing *UI Library* with a different, often newer, version. 
 * same as above, ensuring you use the correct version to name the folder, and update *webapp/ui_library.json* accordingly 

### Delete an existing *UI Library*:
 * remove the library reference(s) from *webapp/ui_library.json*.
 * do not make any changes to the *ui_library Github repository*.
 * check in the *webapp/ui_library.json* file.
 * build the *iq_poc* client.
  
### Build
 * the build script *webapp/tasks/dl-install-libs.js* script the logic required to synchronize the *[ui_libraries](https://github.com/Dematiclabs/ui_librariy)* repository with the application *webapp/vendor* and *webapp/spec* folders. It is triggered during the *mvn clean install* process.