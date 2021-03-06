## Bonus: Additional Login Features

### Goals

* Understand how to create a cookie with user information in it
* Understand how to logout the user

### Code from Previous Chapter

<div class="alert alert-danger" role="alert">Skip this section if you completed the previous chapter</div>

If you have not completed the previous chapter you can get the completed code by downloading the code from Github or open it in StackBlitz.

<h4 class="exercise-start">
    <b>Exercise</b>: Get Previous Code
</h4>

#### StackBlitz Online IDE

If you are using StackBlitz the previous chapter code is avavilable for StackBlitz at [https://stackblitz.com/github/digitaldrummerj/angular-tutorial-code/tree/chapter-additional-todo](https://stackblitz.com/github/digitaldrummerj/angular-tutorial-code/tree/chapter-additional-todo).

#### Downloading Code from Github

1. Downloading and extracting the zip file into your projects folder (c:\projects or ~/projects) at [https://github.com/digitaldrummerj/angular-tutorial-code/archive/chapter-additional-todo.zip](https://github.com/digitaldrummerj/angular-tutorial-code/archive/chapter-additional-todo.zip)
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

### Caching User

Right now we are not caching any user information.  It would be nice to be able to display the user information in the header.  We can cache the user data using cookies.  To implement the cookie storage we are going to use the ngx-cookie library.

<h4 class="exercise-start">
    <b>Exercise</b>: Create Class
</h4>

In the AuthService, in order to hold our user data and get type checking we need to create a TypeScript class with an email and id field.  We are going to leave the password field out of the class as we do not want to store this in memory at all.

1. Within VS Code, open up the integrated terminal (ctrl+`) or view menu and then "Integrated Terminal"
1. Run the ng generate command below to create the Authorization service.  I like to store my services under a shared\services folder.

    ```bash
    ng generate class shared/classes/User
    ```

1. The generate command will the user.ts file in the shared/classes folder:

    ![output of generate](images/user-generate.png)

1. Open the src\app\shared\classes\User.ts file

    ```bash
    user.ts
    ```

1. Within the User class, add the following fields.  Note that the  createdAt and updatedAt are automatically added by the API.

    ```TypeScript
    email: string;
    id: string;
    createdAt: Number;
    updatedAt: Number;
    ```

1. Within the User class and after the fields we just added, create a constructor that requires an email and make an id field optional (hint: the `?` makes the parameter optional)

    ```TypeScript
   constructor(email: string, id?: string, createdAt?: Date, updatedAt?: Date) {
        this.email = email;
        this.id = id;
        this.createdAt = createdAt ? createdAt.getTime() : new Date().getTime();
        this.updatedAt = updatedAt ? updatedAt.getTime() : new Date().getTime();
    }
    ```

<div class="exercise-end"></div>

<h4 class="exercise-start">
  <b>Exercise</b>: Install ngx-cookie
</h4>

1. Open terminal and add/install the ngx-cookie library

  ```bash
  npm install --save ngx-cookie
  ```

1. Open src\app\app.module.ts

    ```bash
    app.module.ts
    ```

1. Import the ngx-cookie library

    ```TypeScript
    import { CookieModule } from 'ngx-cookie';
    ```

1. Add the ngx-cookie library to the @Ngmodule imports sections

    ```TypeScript
    CookieModule.forRoot()
    ```
<div class="exercise-end"></div>

<h4 class="exercise-start">
    <b>Exercise</b>: Add Cookie Get/Set Functions
</h4>

1. Open the auth.service.ts file

    ```bash
    auth.service.ts
    ```

1. Import the User class that we created earlier

    ```TypeScript
    import { User } from '../classes/user';
    ```

1. Import the CookieService from ngx-cookie

    ```TypeScript
    import { CookieService } from 'ngx-cookie';
    ```

1. Update the constructor to inject the CookieService

    ```TypeScript
    constructor(private http: HttpClient, private cookieService: CookieService) {}
    ```

1. Add a class level variable to store the name of the cookie and set it to currentUser

    ```TypeScript
    private cookieKey = 'currentUser';
    ```

1. Add the following functions to get/set the cookie to the AuthService class

    ```TypeScript
    getUser(): User {
        return <User>this.cookieService.getObject(this.cookieKey)
    }

    private setUser(value: User): void {
        this.cookieService.putObject(this.cookieKey, value);
    }

    private clearUser() : void {
        this.cookieService.remove(this.cookieKey);
    }
    ```

<div class="exercise-end"></div>

<h4 class="exercise-start">
    <b>Exercise</b>: Setting Cookie
</h4>

In the auth.service.ts file, we need to change the return type for login, signup, isAuthenticated, to type `<Boolean | User>`

1. Change the return type of the methods to be either Boolean or User.

    ```TypeScript
    <Boolean | User>
    ```

1. Update the http calls to specify the return types.  The format of the call is `this.http.verb<type>`.  For example `this.http.put<User>`

    * Get Example (isAuthenticated)

        ```TypeScript
        return this.http.get<User>(`${this.url}/identity`, requestOptions).pipe(
            tap((user: User) => {
            .......
        }
        ```

    * Put Example (Login)

        ```TypeScript
        return this.http.put<User>(`${this.url}/login`, loginInfo, requestOptions).pipe(
              tap((user: User) => {
              ............
        }
        ```

    * POST Example (signup)

        ```TypeScript
        return this.http.post<User>(this.url, loginInfo, requestOptions).pipe(
            tap((user: User) => {
            .......
            }
        }
        ```

1. In the login, signup, and isAuthenticated functions, add a call to setUser before the return Observable.of(true) statement

    ```TypeScript
    this.setUser(user);
    ```

1. In the login and isAuthenticated functions, before the Observable.of(false) in both the result and catch section add to clearUser since the login was invalid and we want to clear out any existing user cookie

    ```TypeScript
    this.clearUser();
    ```

<div class="exercise-end"></div>

<h4 class="exercise-start">
    <b>Exercise</b>: Display logged in user
</h4>

1. Open header.component.ts

    ```bash
    header.component.ts
    ```

1. Import the AuthService so that we can call the getUser function

    ```TypeScript
    import { AuthService } from '../services/auth.service';
    ```

1. Add the AuthService to the constructor

    ```TypeScript
    constructor(private authService: AuthService) { }
    ```

1. Add a variable to hold the logged in user

    ```TypeScript
    loggedInUser = this.authService.getUser();
    ```

1. Open the src\app\shared\header\header.component.html

    ```bash
    header.component.html
    ```

1. Inside of the `<div class="collapse navbar-collapse"....` tag add the following after the closing `</ul>`

    ```html
    <ul class="navbar-nav navbar-light navbar-expand-md">
        <li class="nav-item nav-link">Welcome {{ loggedInUser?.email }}</li>
    </ul>
    ```

    * This code will display a Welcome along with the email if it is populated.

<div class="exercise-end"></div>

### Logout User

Before being able to signup for an account, we need the user to be logged out first.

There are a number of ways that you could implement this such as giving a logout button in the header or showing user info in header with link to profile page with a logout button.

We are going to implement the logout button in the header.

<h4 class="exercise-start">
    <b>Exercise</b>: Create AuthService Logout
</h4>

1. Open the auth.service.ts file

    ```bash
    auth.service.ts
    ```

1. Add the logout function below that will call the API logout function and clear out the cookie

    ```TypeScript
    logout(): Observable<boolean | Response> {
        return this.http
        .get(`${this.url}/logout`, requestOptions)
        .pipe(
            tap((res: Response) => {
                this.clearUser();
                if (res.ok) {
                    return of(true);
                }

                return of(false);
           }),
            catchError((error: HttpErrorResponse) => {
                this.clearUser();
                return of(false);
            })
        );
    }
`  ```

<h4 class="exercise-start">
    <b>Exercise</b>: Add Logout Button
</h4>

1. Open the src\app\shared\header\header.component.html

    ```bash
    header.component.html
    ```

1. After the "Welcome" tag add the following link tag to call the logout service.  Also, only show the button if the user is logged in.

    ```html
    <li class="nav-item">
        <a class="nav-link" [hidden]="!loggedInUser" (click)="logout()">logout</a>
    </li>
    ```

<div class="exercise-end"></div>

<h4 class="exercise-start">
    <b>Exercise</b>: Add Component Logging Out Function
</h4>

1. Open header.component.ts

    ```bash
    header.component.ts
    ```

1. Import the AuthService and Router

    ```TypeScript
    import { Router } from '@angular/router';
    ```


1. Add the Router to the constructor
    ```TypeScript
    constructor(private authService: AuthService, private router: Router) { }
    ```

1. Add the logout function

    ```TypeScript
    logout() {
        this.authService.logout().subscribe(() => {
            this.router.navigate(['/login']);
        });
    }
    ```

1. You are now ready to test it.

<div class="exercise-end"></div>
