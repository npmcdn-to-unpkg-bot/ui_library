#### Introduction
Our goal is to prevent the artifacts used to build and run a client [Node Modules, Angular Modules, Javascript libraries, fonts, ect], hereon referred to as *library(ies)*, from being committed to the source repository, while seamlessly:
 * supporting the management of these *libraries* during the *UI software construction processw*.
 * installing or updating the *libraries* during *maven builds*.

#### Elements
Our solution elements include:
 * *[linemanjs](http://linemanjs.com/)* - our development framework
 * *[bower](http://bower.io/)*, a package manger used to help us find a *library's* location. 
 * *[ui_libraries](https://github.com/Dematiclabs/ui_libraries)* - Repository including the css, fonts, and ja libraries.
 * *iq_poc/ngclient/src/main/webapp/vendor* the folder where the *ui libraries* are installed.
 * *dl-install-libs*, a custom *[grunt](http://gruntjs.com/)* task that uses the [grunt-exec](https://www.npmjs.com/package/grunt-exec) plugin to install all *libraries*.
 * *.gitignore*, a git file including a configuration to ignore the *iq_poc/ngclient/src/main/webapp/vendor* folder.
 * *[maven-exec](http://www.mojohaus.org/exec-maven-plugin/)*, a maven plugin used execute a build step to load the library 

#### Workflow

##### Development
##### Set up the client library lcoal repository
 * create a folder to hold the *[ui_libraries](https://github.com/Dematiclabs/ui_libraries)* local repository; I used I used *~/Projects/client_libraries*. 
 * clone the *[ui_libraries](https://github.com/Dematiclabs/ui_libraries)* repository.

##### Add a new library to the *[ui_libraries](https://github.com/Dematiclabs/ui_libraries)* repository:
 * navigate to the *[ui_libraries](https://github.com/Dematiclabs/ui_libraries)* local repository.
 * pull from the *[ui_libraries](https://github.com/Dematiclabs/ui_libraries)* repository. 
 * find the desired *library*; you might have to use *[bower](http://bower.io/)* to download the *library* in a work folder.
 * identify the *library's*files of interest - often only a subset is required.
 * copy the identified files to the *[ui_libraries](https://github.com/Dematiclabs/ui_libraries)* local repository's *vendor/css*, *vendor/static/fonts*, and *js* folders.
 * commit and check in the changes to the *[ui_libraries](https://github.com/Dematiclabs/ui_libraries)* repository.

##### Update an existing library:
 * navigate to the *[ui_libraries](https://github.com/Dematiclabs/ui_libraries)* local repository.
 * pull from the *[ui_libraries](https://github.com/Dematiclabs/ui_libraries)* repository. 
 * find the desired *library*; you might have to use *[bower](http://bower.io/)* to download the *library* in a work folder.
 * identify the *library's*files of interest - often only a subset is required.
 * copy the identified files to the *[ui_libraries](https://github.com/Dematiclabs/ui_libraries)* local repository's *vendor/css*, *vendor/static/fonts*, and *js* folders.
 * commit and check in the changes to the *[ui_libraries](https://github.com/Dematiclabs/ui_libraries)* repository.

##### Delete an existing library:
 * navigate to the *[ui_libraries](https://github.com/Dematiclabs/ui_libraries)* local repository.
 * pull from the *[ui_libraries](https://github.com/Dematiclabs/ui_libraries)* repository. 
 * identify the *library's*files to be deleted.
 * delete the identified files from the *[ui_libraries](https://github.com/Dematiclabs/ui_libraries)* local repository's *vendor/css*, *vendor/static/fonts*, and *js* folders.
 * commit and check in the changes to the *[ui_libraries](https://github.com/Dematiclabs/ui_libraries)* repository.
  
##### Build
 * there is no additional work required during the build process