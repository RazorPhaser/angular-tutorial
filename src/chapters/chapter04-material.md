## Angular Material

### Overview

For our styling we are going to use [Angular Material](https://material.angular.io/).

### Goals

* Understand how to include Material into our project

### Install Material

<h4 class="exercise-start">
    <b>Exercise</b>: Install Material
</h4>

1. In the VS Code Integrated Terminal, click the + to open a 2nd terminal
1. Run the Angular CLI command to add Material

    ```bash
     ng add @angular/material
     ```

Before we can use Material we need to add it to the AppModule.  The suggested way to do this is to create a module just for Material

1. In the terminal window, run the following command to create a new module called in material in the shared folder

    ```bash
    ng generate module shared/material --flat --spec false
    ```

1. Open the src\app\shared/material.module.ts

    <div class="alert alert-info" role="alert">In Visual Studio Code you can quickly open a file by using ctrl+p to open the "Go To File" prompt and typing in the file name</div>

    ```bash
    material.module.ts
    ```

1. Import the Material components at the top of the file

    ```TypeScript
    import {
    MatButtonModule,
    MatInputModule,
    MatFormFieldModule,
    MatMenuModule,
    MatToolbarModule,
    MatListModule,
    MatIconModule,
    MatTooltipModule,
    } from '@angular/material';
    ```

1. In the @NgModule imports section add the Material modules

    ```TypeScript
    CommonModule,
    MatButtonModule,
    MatInputModule,
    MatListModule,
    MatIconModule,
    MatToolbarModule,
    MatFormFieldModule,
    MatMenuModule,
    MatTooltipModule,
    ```

1. In the @NgModule, we need to add an exports section and include the Material modules that we imported

    ```TypeScript
    exports: [
        MatButtonModule,
        MatInputModule,
        MatListModule,
        MatIconModule,
        MatToolbarModule,
        MatFormFieldModule,
        MatMenuModule,
        MatTooltipModule,
    ],
    ```

Now we need to add the Material module to the App Module

1. Open the src/app/app.module.ts file

    ```bash
    app.module.ts
    ```

1. In the @NgModule imports section add the Material module

    ```TypeScript
    MaterialModule
    ```

1. Visual Studio Code will complain that is does not know what the MaterialModule is.  To fix this, put your cursor on the text MaterialModule and click ctrl+. to bring up the lightbulb help and select add MaterialModule

<div class="exercise-end"></div>

### Add Material Theme

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
