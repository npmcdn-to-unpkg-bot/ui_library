#### Introduction
Our goal is to segregate the *CSS, FONT, HTML, and JS* 3rd party artifacts, hereon referred to as *artifacts*, used to run the *application client* into their own repository, separate from the *application source repository* , while seamlessly:
 * supporting the management of these *artifacts* during the *UI software construction process*.
 * installing or updating the *artifacts* during *maven builds*.
 * maintaining version integrity.

#### Elements
Our solution elements include:
 * *[Node](https://nodejs.org/en/)* - Node.js is a JavaScript runtime built on Chrome's V8 JavaScript engine. It is used to support the UI construction effort; it is not required to run the application. This document assumes the reader is thouroughly familar with [Node](https://nodejs.org/en/) and its modular architecture.
 * *[linemanjs](http://linemanjs.com/)* - the development framework used to build the application UI.
 * *[grunt](http://gruntjs.com/)* - the javascript task runner.
 * *[ui_libraries](https://github.com/Dematiclabs/ui_libraries)* - repository including the artifacts.
 * *iq_poc/ngclient/src/main/webapp/vendor* - the folder where the *artifacts* are installed.
 * *.gitignore*, a git file including a configuration to ignore the *iq_poc/ngclient/src/main/webapp/vendor* folder.
 * *[maven-exec](http://www.mojohaus.org/exec-maven-plugin/)*, a maven plugin used execute a build step to load the *artifacts*. 

#### Highlights
The solution consists in harnessing the *3rd party ui artifacts* required to run the application in their own *[ui libratries](https://github.com/Dematiclabs/ui_libraries)* repository, distinct from the *application repository*. When a new *3rd party ui artifact* is required or an existing *3rd party ui artifact* needs to be updated, the work is done in the **ui artifact** local repository and checked in the *[ui libraries](https://github.com/Dematiclabs/ui_libraries)* repository. The build scripts include logic to extract the *3rd party ui artifact(s)* from the *[ui libratries](https://github.com/Dematiclabs/ui_libraries)* repository and integrate them into the application *vendor* folder.

#### Workflow

##### Development
##### Set up the client library lcoal repository
 * create a folder to hold the *[ui_libraries](https://github.com/Dematiclabs/ui_libraries)* local repository; I used I used *~/Projects/client_libraries*. 
 * clone the *[ui_libraries](https://github.com/Dematiclabs/ui_libraries)* repository.

##### Add a new library to the *[ui_libraries](https://github.com/Dematiclabs/ui_libraries)* repository:
 * install the *artifacts* in your *iq_poc/ngclient/src/main/webapp/vendor* sandbox and test them thoroughly.
 * navigate to the *[ui_libraries](https://github.com/Dematiclabs/ui_libraries)* local repository.
 * create a working branch
 * refresh the *[node_modules](https://github.com/Dematiclabs/node_modules)* repository. 
 * install the desired *3rd party ui artifact(s)* in the local repository's *vendor/css*, *vendor/fonts/static*, and *vendor/js* folders.
 * commit and check in the changes to the *[ui_libraries](https://github.com/Dematiclabs/ui_libraries)* repository.

##### Update an existing library:
 * navigate to the *[ui_libraries](https://github.com/Dematiclabs/ui_libraries)* local repository.
 * refresh the *[node_modules](https://github.com/Dematiclabs/node_modules)* repository. 
 * update the desired *3rd party ui artifact(s)* in the local repository's *vendor/css*, *vendor/fonts/static*, and *vendor/js* folders.
 * commit and check in the changes to the *[ui_libraries](https://github.com/Dematiclabs/ui_libraries)* repository.

##### Delete an existing library:
 * navigate to the *[ui_libraries](https://github.com/Dematiclabs/ui_libraries)* local repository.
 * refresh the *[node_modules](https://github.com/Dematiclabs/node_modules)* repository. 
 * delete the desired *3rd party ui artifact(s)* from the local repository's *vendor/css*, *vendor/fonts/static*, and *vendor/js* folders.
 * commit and check in the changes to the *[ui_libraries](https://github.com/Dematiclabs/ui_libraries)* repository.
  
##### Build
 * the build process *dl-install-libs* script contains the logic required to synchronized the *[ui_libraries](https://github.com/Dematiclabs/ui_libraries)* repository with the application *vendor* folder.