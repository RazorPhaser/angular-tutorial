## Getting up and running

### Overview

To get started, we need to install and configure the following software first.

* Supported Platforms: Windows, Mac, or Linux computer
* Editor: Visual Studio Code (can use any text editor but workshop tested with Visual Studio Code)
* Software:
  * Node 8
  * Angular CLI

### Goals

* Setup your machine for the Workshop

### StackBlitz Online IDE

If you would prefer to not install anything on your computer and want to develop 100% in the browser with a Visual Studio Code like editor, you can use StackBlitz.  Each lab has a link to StackBlitz for a starting point for that lab.

<div class="alert alert-danger" role="alert">Skip to <a href='#chapter3'>creating the project</a> if you are using StackBlitz</div>

### Windows Showing File Extensions

<div class="alert alert-danger" role="alert">
**Windows Only**
</div>

**Non-Windows users can [skip to next section](#chapter2.4)**

By default Windows is set to not show file extensions for known files which causes files such as .gitconfig and .npmrc to show up as just a period with no file extension which makes it extremely difficult to figure out what the file actually is. To fix this we need to turn set Windows Explorer to show file extensions.

<h4 class="exercise-start">
    <b>Exercise</b>: Turn On Windows Showing File Extensions
</h4>

1. Open Windows Explorer
1. Click on the View Tab and select Options

    <img src="images/chapter1/windows-explorer-ribbon.png" style="height:147px;width:759px;margin-left: 10px">

Once the "Folder Options" dialog is open:

1. Click on the View Tab
1. Uncheck the "Hide extensions for known file types"
1. Click Ok

    <img src="images/chapter1/windows-explorer-view-options.png" style="height:475px;width:382px;margin-left: 10px">

<div class="exercise-end"></div>

### Visual Studio Code

Visual Studio Code is Microsoft lightweight cross platform IDE.

<h4 class="exercise-start">
    <b>VSCode Setup</b>
</h4>

1. Download Visual Studio Code at [https://code.visualstudio.com/](https://code.visualstudio.com/)
1. Once the download finishes, launch the installer except all of the defaults.
1. Here are the extensions that I have installed:

    * [Angular v6 Snippets](https://marketplace.visualstudio.com/items?itemName=johnpapa.Angular2)
    * [Angular 2 Switcher](https://marketplace.visualstudio.com/items?itemName=infinity1207.angular2-switcher)
    * [Angular Language Service](https://marketplace.visualstudio.com/items?itemName=Angular.ng-template)
    * [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
    * [Path Intellisense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.path-intellisense)
    * [Bracket Pair Colorizer](https://marketplace.visualstudio.com/items?itemName=CoenraadS.bracket-pair-colorizer)
    * [Editor Config](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig)
    * [TSLint](https://marketplace.visualstudio.com/items?itemName=eg2.tslint)
    * [REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client)
    * [Setting Sync](https://marketplace.visualstudio.com/items?itemName=Shan.code-settings-sync)

1. To hide the mini map go into the Preferences -> Settings (File -> Preferences -> Settings on Windows) and add the following setting

    ```bash
    "editor.minimap.enabled": false,
    ```

1. I also like to always have word wrap turned on.  You can turn this on in the same preferences file as you used for turning off the mini map above.

    ```bash
    "editor.wrappingIndent": "same",
    ```

1. Prettier settings that take effect when formatting the document

    ```json
    "prettier.printWidth": 100,
    "prettier.singleQuote": true,
    "prettier.bracketSpacing": true,
    "prettier.trailingComma": "es5",
    ```

1. Some people also like to have VSCode auto save the file for them.  Below is will save the file anytime that you switch to a different file or different program.  You can also do `ctrl+s` at anytime to save the file as well

    ```json
    "files.autoSave": "onFocusChange"
    ```

<div class="exercise-end"></div>


### Node.js

NodeJS is used to power the Angular CLI as well as install all of our dependencies. The Angular CLI requires Node version 8.

1. Download the latest stable version (LTS) of [NodeJS](http://nodejs.org) which as of this writing is 8.11.1.
1. Run the installer and accept all defaults.
1. Verify that Node installed. Start a command prompt or terminal window and run:

<h4 class="exercise-start">
    <b>Exercise</b>: Verify Node Install
</h4>

```bash
node -v
```

<div class="exercise-end"></div>

### Angular CLI Install

The Angular CLI (Command Line Interface) makes it so that you do not have to worry about the Angular tooling and can focus instead on your code. You can create new projects, components, modules, services, guards, pipes and routes. As well it has commands for linting, testing and running our code.

All of the code that is generated by the Angular CLI following the Angular Style Guide.

While you do not have to use the Angular CLI, it is highly recommended, will increase your productivity, and this workshop only gives the instructions for developing with the Angular CLI.

<h4 class="exercise-start">
    <b>Exercise</b>: Install Angular CLI
</h4>

<div class="alert alert-info" role="alert">This workshop has been tested against Angular CLI 6.0.0</div>

1. Open a command prompt or terminal and run the following command

    ```bash
    npm install -g @angular/cli
    ```

1. Verify Angular CLI

    ```shell
    ng --version
    ```

    ![ng version output](images/chapter1/ng-version.png)

<div class="exercise-end"></div>
