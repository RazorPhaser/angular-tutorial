## Create New Project

### Overview

In this chapter we will be creating our project with the Angular CLI.  We will use this project throughout the workshop.

### Goals

* Understand how to create a new project
* Understand how to find help for an Angular CLI command
* Understand the project layout
* Understand how to run the project

### StackBlitz Online IDE

The generated project is available for StackBlitz at [https://stackblitz.com/github/digitaldrummerj/angular-tutorial-code/tree/chapter-project-created](https://stackblitz.com/github/digitaldrummerj/angular-tutorial-code/tree/chapter-project-created).

<div class="alert alert-danger" role="alert">Skip to <a href='#chapter3.4'>project layout</a> if you are using StackBlitz</div>

### Generate New Project

The project that the Angular CLI create for you follows all of the suggested standards and has webpack for bundling built-in to it.

<h4 class="exercise-start">
    <b>Exercise</b>: Create Angular Project
</h4>

1. Open a command prompt
1. Navigate to where you want to store your project files.  I use c:\projects on Windows and ~/projects on OSx.  You are free to use anywhere that you want.

    * Windows:

        ```bash
        cd \
        ```
    * OSx:

        ```bash
        cd ~/
        ```

1. Create the projects directory.  If you already have a directory that you store your projects in then you can skip this step.

    ```bash
    mkdir projects
    ```

1. Navigate into the projects directory

    ```bash
    cd projects
    ```

1. Generate a project named ngws that uses scss for styling and includes a routing file by running

    ```bash
    ng new ngws --style scss --routing
    ```

    **Sample Output:**
    ![ng new](images/ng-new.png)

1. If you want to see the other ng new options or any Angular CLI command append the --help

    ```bash
    ng new --help
    ```

<div class="exercise-end"></div>

### Opening Project in Visual Studio Code

1. Open Visual Studio Code
1. Click File -> Open Folder...
1. Navigate to angular-tutorial directory and click Select Folder
1. Your project should now be opened in Visual Studio Code

    ![Project Layout](images/project-layout.png)

### Running Project

<h4 class="exercise-start">
    <b>Exercise</b>: Run the project
</h4>

The Angular CLI has a built-in command for starting up a development web server for your project called `ng serve` which will run webpack to bundle up your code, start the development web server, rebuild on file changes (watch) and refresh connected browsers (live reload).

1. Visual Studio Code has a built-in terminal that we can use to run our commands.  On Windows, this is a powershell prompt.  To open the Integrated Terminal go under the View Menu and click on the Integrate Terminal or press Ctrl+`
    * You are free to use the regular command prompt outside of Visual Studio Code if you would like
1. Will be using the package.json shortcut scripts to run our commands.  Personally, I like to setup my package.json scripts to run all of my commands like linting, testing, build, and running.  Out of the box, the package.json scripts are setup for these.  Later, we will modify them to add additional functionality for running continuous integration scripts.

    ```bash
    npm run start
    ```

    ![ng serve output](images/ng-serve.png)

    <div class="alert alert-info" role="alert">The npm run start (ng serve) command will stay running in order to provide live reloading functionality.</div>

    <div class="alert alert-danger" role="alert">Sometimes ng serve gets into a state where it complains that something is wrong but you swear your code it right.  If this happens, the first troubleshooting step is to stop npm run start by using ctrl+c and then execute npm run start again.  If it still errors out, then there is something wrong with your code.</div>

1. If you launch your browser and navigate to [http://localhost:4200](http://localhost:4200), you will see a page that looks like

    ![app works](images/appworks.png)

<div class="exercise-end"></div>

### Navigating around Visual Studio Code

Being able to effectively use your edit or is key to being a super productive developer.  With Visual Studio Code, there are several shortcut keys that will help you out.

| Purpose | Key |
| ---- | ---- |
| Integrated Terminal | ctrl+` |
| Open File | ctrl+p |
| Switch Between Files | ctrl+tab |
| Switch Between Files Reverse | ctrl+shift+tab |
| Hide Side Menu | ctrl+b |
| Toggle Word Wrap for File  | alt+z |
| Format Document | ctrl+alt+f |
| Save All | ctrl+shift+s |

<div class="alert alert-info" role="alert"> I also split my screen in half with the tutorial on one side and the editor on the other side.  On Windows you can do this by using the win key + left arrow for the one you want on the left and then select the other for the right when windows prompts you.  You can also use win key + right arrow to make a Windows use half the screen on the right.</div>

### Review

In this chapter we learned 3 things

1. How to create a new projects using the `ng new` command
1. What the project layout looks like for an Angular project generated with the CLI
1. How to run our project with the `ng serve` command and view it at [http://localhost:4200](http://localhost:4200)
