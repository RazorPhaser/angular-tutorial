## Bootstrap

### Overview

For our styling we are going to use [Bootstrap 4](https://getbootstrap.com/).  The reason for picking Bootstrap 4 and not Bootstrap 3 is so that we can use [Angular Bootstrap library (ng-bootstrap)](https://ng-bootstrap.github.io).  ng2-bootstrap is written 100% in JavaScript with no need for JQuery or Bootstrap's JavaScript library to be included.

### Goals

* Understand how to include Bootstrap 4 into your project

### Install Bootstrap

<h4 class="exercise-start">
    <b>Exercise</b>: Install Bootstrap
</h4>

1. In the VS Code Integrated Terminal, click the + to open a 2nd terminal
1. Run the npm install command for bootstrap and font-awesome

    ```bash
    npm install --save @fortawesome/fontawesome-svg-core @fortawesome/free-solid-svg-icons @fortawesome/angular-fontawesome @fortawesome/free-regular-svg-icons bootstrap @ng-bootstrap/ng-bootstrap
    ```

    * This will install ng-bootstrap along with bootstrap and font-awesome.  Bootstrap is still required for ng-bootstrap to work.

Before we can use ng-bootstrap we need to add it to the AppModule

1. Open the src\app\app.module.ts

    <div class="alert alert-info" role="alert">In Visual Studio Code you can quickly open a file by using ctrl+p to open the "Go To File" prompt and typing in the file name</div>

    ```bash
    app.module.ts
    ```

1. Import the NgbModule from @ng-bootstrap/ng-bootstrap and AngularfontAwesomeModule from angular-font-awesome

    ```TypeScript
    import {NgbModule} from '@ng-bootstrap/ng-bootstrap';
    import { FontAwesomeModule } from '@fortawesome/angular-fontawesome';
    ```

1. In the @NgModule imports section add NgbModule.forRoot() and AngularFontAwesomeModule

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

1. In the src\app folder, create a file called **_variables.scss**

      <div class="alert alert-info" role="alert">You can create file right in Visual Studio Code by right-click on the src\app folder</div>

    ```bash
    _variables.scss
    ```

1. Add the following to the src\app\_variables.scss file

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

1. In the app folder, open the file src\app\style.scss

    ```bash
    style.scss
    ```

1. Add the following contents to the src\app\style.scss file to setup the site wide styles using our variables and the bootstrap styles

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

<div class="exercise-end"></div>

### View Changes

<div class="alert alert-danger" role="alert">Since we already had ng serve running, it picked up the html changes but you will notice that there is no styling.  This is because whenever you change the .angular-cli.json file, you need to restart ng serve before they take effect.</div>

<h4 class="exercise-start">
    <b>Exercise</b>: Restart ng serve
</h4>

1. Go to the integrated terminal in Visual Studio Code that is running the `ng serve` command and do a ctrl+c to stop it.

    > There is a dropdown on the right side of the Visual Studio Code integrated terminal that allows you to change to the other terminals that are currently open for your project

1. Run the `ng serve` command again.

    ```bash
    ng serve
    ```

1. The web page should now look like

    ![App Works with Bootstrap](images/bootstrap-jumbotron.png)

<div class="exercise-end"></div>

### Review

In this chapter we learned how to use Bootstrap for our project.

Learned:

1. How to install Bootstrap 4 and font-awesome
1. How to integrate it into the Angular CLI in the .angular-cli.json file
1. How to create our own custom Bootstrap SCSS variables to override the built-in styles of Bootstrap with our own colors
1. How to create a banner at the top of the page
1. How to change the text that appears in the banner using our TypeScript title variable
1. Learned that when you modify the .angular-cli.json file that you have to restart `ng serve` for the changes to take effect