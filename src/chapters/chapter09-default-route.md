## Implementing Default Route

### Overview

Right now if the user types in a route that Angular does not know about you will get the following error

![no route found](images/ng2/no-route-found.png)

I prefer to solve this problem by creating a "Not Found" component and then redirecting the user to this component if they try to navigate to a route that does not exist.

### Goals

* Understand how to deal with an unknown route

### Code from Previous Chapter

<div class="alert alert-danger" role="alert">Skip this section if you completed the previous chapter</div>

If you have not completed the previous chapter you can get the completed code by downloading the code from Github or open it in StackBlitz.

<h4 class="exercise-start">
    <b>Exercise</b>: Get Previous Code
</h4>

#### StackBlitz Online IDE

If you are using StackBlitz the previous chapter code is avavilable for StackBlitz at [https://stackblitz.com/github/digitaldrummerj/angular-tutorial-code/tree/chapter-env-config](https://stackblitz.com/github/digitaldrummerj/angular-tutorial-code/tree/chapter-env-config).

#### Downloading Code from Github

1. Downloading and extracting the zip file into your projects folder (c:\projects or ~/projects) at [https://github.com/digitaldrummerj/angular-tutorial-code/archive/chapter-env-config.zip](https://github.com/digitaldrummerj/angular-tutorial-code/archive/chapter-env-config.zip)
1. After you get the code, run npm install to get all of the NPM dependencies.

    ```bash
    npm install
    ```

1. Open Visual Studio Code
1. In Visual Studio Code, go under the File menu, select Open folder and navigate to the folder that you unzipped the files into
1. If you have ng serve running in a different editor, make sure to stop it from running.
1. Open the Integrated Terminal in Visual Studio Code (ctrl + `)  and run ng serve

    ```bash
    ng serve
    ```

<div class="exercise-end"></div>

### Create Not Found Component

<h4 class="exercise-start">
    <b>Exercise</b>: Redirecting User to "Not Found" component
</h4>

1. Open the integrated terminal and generate the notFound component

    ```bash
    ng generate component notFound
    ```

1. 4 files are created just like when we created the TodoComponent earlier.  You will notice this time though that the Angular Cli put a dash between not and found.  It will automatically do that when it encounters an uppercase character.

    ![not found generated file list](images/ng2/notfound-generated.png)

1. Open src\app\app-routing.module.ts

    ```bash
    app-routing.module.ts
     ```

1. add an import statement for the NotFoundComponent

    ```TypeScript
    import { NotFoundComponent } from './not-found/not-found.component';
    ```

1. Add the ** route to and set it to use the NotFoundComponent

    ```TypeScript
    { path: '**', component: NotFoundComponent }
    ```

1. Your routes should look like so

    ```TypeScript
    const routes: Routes = [
        {
            path: '',
            component: TodoComponent,
            canActivate: [IsLoggedInGuard]
        },
        { path: 'login', component: LoginComponent },
        { path: 'signup', component: SignupComponent },
        { path: '**', component: NotFoundComponent }
    ];
    ```

1. If you now try to navigate to [http://localhost:4200/unknown](http://localhost:4200/unknown) you will be shown the NotFoundComponent

    ![Not Found View](images/view-route-unknown.png)

The only thing left for you to do is to design what you want your not found page to actually say.
