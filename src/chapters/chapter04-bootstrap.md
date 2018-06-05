## Bootstrap

### Overview

For our styling we are going to use [Bootstrap 4](https://getbootstrap.com/).  The reason for picking Bootstrap 4 and not Bootstrap 3 is so that we can use [Angular Bootstrap library (ng-bootstrap)](https://ng-bootstrap.github.io).  ng2-bootstrap is written 100% in JavaScript with no need for JQuery or Bootstrap's JavaScript library to be included.

### Goals

* Understand how to include Bootstrap 4 into your project

### Code from Previous Chapter

<div class="alert alert-danger" role="alert">Skip this section if you completed the previous chapter on your local computer or in StackBlitz</div>

<h4 class="exercise-start">
    <b>Exercise</b>: Get Previous Code
</h4>

#### Using StackBlitz Online IDE

If you are using StackBlitz the previous chapter code is avavilable for StackBlitz at [https://stackblitz.com/github/digitaldrummerj/angular-tutorial-code/tree/chapter-project-created](https://stackblitz.com/github/digitaldrummerj/angular-tutorial-code/tree/chapter-project-created).

### Install Bootstrap

1. In the VS Code Integrated Terminal, click the + to open a 2nd terminal
1. Run the npm install command for bootstrap and font-awesome

    ```bash
    npm install --save @fortawesome/fontawesome-svg-core @fortawesome/free-solid-svg-icons @fortawesome/angular-fontawesome @fortawesome/free-regular-svg-icons bootstrap @ng-bootstrap/ng-bootstrap rxjs-compat
    ```

    * This will install ng-bootstrap along with bootstrap and font-awesome.  Bootstrap is still required for ng-bootstrap to work.
    * Yes, it really is called @fortawesome and not @fontawesome

    > rxjs-compat is required until ngx-bootstrap updates to rxjs 6.0

Before we can use ng-bootstrap we need to add it to the AppModule

1. Open the src\app\app.module.ts

    <div class="alert alert-info" role="alert">In Visual Studio Code you can quickly open a file by using ctrl+p to open the "Go To File" prompt and typing in the file name</div>

    ```bash
    app.module.ts
    ```

1. Import the NgbModule from @ng-bootstrap/ng-bootstrap and FontAwesomeModule from @fortawesome/angular-fontawesome

    ```TypeScript
    import {NgbModule} from '@ng-bootstrap/ng-bootstrap';
    import { FontAwesomeModule } from '@fortawesome/angular-fontawesome';
    ```

1. In the @NgModule imports section add NgbModule.forRoot() and FontAwesomeModule

    ```TypeScript
    NgbModule.forRoot(),
    FontAwesomeModule
    ```

<div class="exercise-end"></div>

### Add Bootstrap to Project

<h4 class="exercise-start">
    <b>Exercise</b>: Add  Bootstrap to Project
</h4>

First we need to create our own custom Bootstrap variables files so that we can override the Bootstrap scss variables to create our own colors and styles using the existing Bootstrap scss variables.

1. In the src folder, create a file called **_variables.scss**

      <div class="alert alert-info" role="alert">You can create file right in Visual Studio Code by right-click on the src folder</div>

    ```bash
    _variables.scss
    ```

1. Add the following to the _variables.scss file

    ```scss
    // Variables
    // Colors
    //
    // Grayscale and brand colors for use across Bootstrap.
    $dark-blue: #003C71;

    // Start with assigning color names to specific hex values.
    $white:  #fff !default;
    $black:  #000 !default;
    $red:    #d9534f !default;
    $orange: #f0ad4e !default;
    $yellow: #ffd500 !default;
    $green:  #5cb85c !default;
    $blue:   #0275d8 !default;
    $teal:   #5bc0de !default;
    $pink:   #ff5b77 !default;
    $purple: #613d7c !default;

    // Create grayscale
    $gray-dark:                 #292b2c !default;
    $gray:                      #464a4c !default;
    $gray-light:                #636c72 !default;
    $gray-lighter:              #eceeef !default;
    $gray-lightest:             #f7f7f9 !default;

    // Reassign color vars to semantic color scheme
    $brand-primary:             $blue !default;
    $brand-success:             $green !default;
    $brand-info:                $teal !default;
    $brand-warning:             $orange !default;
    $brand-danger:              $red !default;
    $brand-inverse:             $gray-dark !default;
    ```

    <div class="alert alert-info" role="alert">To create your own theme for Bootstrap following the instructions at <a href='https://getbootstrap.com/docs/4.1/getting-started/theming/'>https://getbootstrap.com/docs/4.1/getting-started/theming/</a></div>

1. In the app folder, open the file src\style.scss

    ```bash
    style.scss
    ```

1. Add the following contents to the src\style.scss file to setup the site wide styles using our variables and the bootstrap styles

    ```scss
    @import "_variables";

    // Bootstrap and its default variables
    @import "~bootstrap/scss/bootstrap";
    ```

<div class="exercise-end"></div>

### Add Banner Section to Top

<h4 class="exercise-start">
    <b>Exercise</b>: Add Banner To Top of Page
</h4>

1. Open src\app\app.component.html

    ```bash
    app.component.html
    ```

1. Replace the contents with:

    ```html
    <div class="jumbotron">
        <div class="container">
            <h1>{{title}}</h1>
        </div>
    </div>
    <div class="container">
        <router-outlet></router-outlet>
    </div>
    ```

1. Lets change the title to something better than "App Works!"

    * Open the src\app\app.component.ts file

        ```bash
        app.component.ts
        ```

    * On line 9, change the title variable to

        ```TypeScript
        title = 'Our Awesome Todo App!';
        ```

1. The web page should now look like

    ![App Works with Bootstrap](images/bootstrap-jumbotron.png)

<div class="exercise-end"></div>

### Review

In this chapter we learned how to use Bootstrap for our project.

Learned:

1. How to install Bootstrap 4 and font-awesome 5
1. How to create our own custom Bootstrap SCSS variables to override the built-in styles of Bootstrap with our own colors
1. How to create a banner at the top of the page
1. How to change the text that appears in the banner using our TypeScript title variable
