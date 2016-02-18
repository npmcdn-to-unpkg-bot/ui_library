#### Introduction
Our goal is to prevent the artifacts used to build and run a client [Node Modules, Angular Modules, Javascript libraries, fonts, ect], hereon referred to as *library(ies)*, from being committed to the source repository, while seamlessly:
 * supporting the management of these *libraries* during the *UI software construction processw*.
 * installing or updating the *libraries* during *maven builds*.

#### Elements
Our solution elements include:
 * *[linemanjs](http://linemanjs.com/)* - our development framework.
 * *[bower](http://bower.io/)*, a package manger used to help us find a *library's* location. 
 * *[DLABS node_modules](https://github.com/Dematiclabs/node_modules)* - Repository including the node modules.
 * *[DLABS ui_libraries](https://github.com/Dematiclabs/ui_libraries)* - Repository including the css, fonts, and ja libraries.
 * *iq_poc/ngclient/src/main/webapp/node_modules*, hereon referred to as *node modules*, the folder where the node modulews* are installed.
 * *iq_poc/ngclient/src/main/webapp/vendor*, hereon referred to as *vendor*, the folder where the *ui libraries* are installed.
 * *dl-install-libs*, a custom *[grunt](http://gruntjs.com/)* task that uses the [grunt-exec](https://www.npmjs.com/package/grunt-exec) plugin to install all *libraries* using.
 * *.gitignore*, a git file including a configuration to ignore the *iq_poc/ngclient/src/main/webapp/vendor* and *iq_poc/ngclient/src/main/webapp/node_modules* folders.
 * *[maven-exec](http://www.mojohaus.org/exec-maven-plugin/)*, a maven plugin used execute a build step to load the library.
