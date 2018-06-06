## Deploying

### Overview

Before deploy you will need to run an a build with the Angular CLI.  With the build you can tell it the environment to use and if it is a production build or not.  A production will minify everything.

### Goals

* Learn how to create a build that is ready to deploy.

### Building Steps

In order to deploy you should run through unit test, linting, end to end testing, and building for the environment.

### Linting

<h4 class="exercise-start">
  <b>Exercise</b>: Linting The Code
</h4>

I am using TeamCity for my CI which means that I need to be able to report out the linting report.

1. Open a terminal and navigate to your Angular project
1. Install the tslint teamcity reporter package

  ```bash
  npm install --save-dev tslint-teamcity-reporter
  ```

1. To run linting in a CI environment, run

  ```bash
  ng lint --format tslint-teamcity-reporter
  ```

<div class="exercise-end"></div>

### Testing

<h4 class="exercise-start">
  <b>Exercise</b>: Unit Testing the Code
</h4>

<div class="alert alert-danger" role="alert">This step will fail as we have not been updating the unit tests. In your own projects outside the workshop, you would want to keep the unit tests updated as you go </div>

1. Open a terminal and navigate to your Angular project
1. Run the following command to run unit testing with code coverage using the Chrome Headless browser

  ```bash
  ng test --single-run --code-coverage=true --browsers ChromeHeadless
  ```

<div class="exercise-end"></div>

### End to End Testing

<h4 class="exercise-start">
  <b>Exercise</b>: End to End Testing Your Code
</h4>

Before we can run our end to end test, we need to create a configuration file to ensure that we run using the Chrome headless browser and set the browser resolution to use.

1. In the root directory of the project, create a file called protractor.conf.ci.js

  ```bash
  protractor.conf.ci.js
  ```

1. Set the contents of the `protractor.conf.ci.js` to the following.  The difference between this file and the protractor.conf.js file is that chromeOptions section.

  ```javascript
  // Protractor configuration file, see link for more information
  // https://github.com/angular/protractor/blob/master/lib/config.ts

  const { SpecReporter } = require('jasmine-spec-reporter');

  exports.config = {
    allScriptsTimeout: 11000,
    specs: ['./e2e/**/*.e2e-spec.ts'],
    capabilities: {
      browserName: 'chrome',
      chromeOptions: {
        args: ['--headless', '--disable-gpu', '--window-size=1280,768'],
      },
    },
    directConnect: true,
    baseUrl: 'http://localhost:4200/',
    framework: 'jasmine',
    jasmineNodeOpts: {
      showColors: true,
      defaultTimeoutInterval: 30000,
      print: function() {},
    },
    onPrepare() {
      require('ts-node').register({
        project: 'e2e/tsconfig.e2e.json',
      });
      jasmine.getEnv().addReporter(new SpecReporter({ spec: { displayStacktrace: true } }));
    },
  };
  ```

1. Open a terminal and navigate to your Angular project
1. To run end to end tests in a CI environment, run

  ```bash
  ng e2e -c protractor.conf.ci.js
  ```

<div class="exercise-end"></div>

### Creating Non-Production Build

<div class="alert alert-info" role="alert">
Note the build create a dist folder to hold the output.   This directory is removed before each build
</div>

<h4 class="exercise-start">
  <b>Exercise</b>: Running Non-Production Build
</h4>

Run the following command to run a build that uses the environment.ts file and is not a production build

```bash
ng build
```

<div class="exercise-end"></div>

### Creating Production Build

<h4 class="exercise-start">
  <b>Exercise</b>: Running a Production Build
</h4>

<div class="alert alert-warning" role="alert">
Note that this will remove the dist directory before build.
</div>

Run the following command to run a build that uses the environment.prod.ts file and is a production build.

```bash
ng build --prod
```

You will now have a production ready deploy in the the dist folder.

<div class="exercise-end"></div>

### Make It Easy to Remember Commands

It can be a pain to remember all of these commands.  I like to update the package.json scripts section to have a script for each of the sections.

1. Open the package.json file

  ```bash
  package.json
  ```

1. Find the scripts section and replace it with the following section

  ```json
  "scripts": {
      "ng": "ng",
      "start": "ng serve",
      "build": "ng build",
      "build:prod": "ng build --prod",
      "test": "ng test",
      "test:ci": "ng test --single-run --code-coverage=true --browsers ChromeHeadless",
      "lint": "ng lint -t stylish",
      "lint:ci": "ng lint --format tslint-teamcity-reporter",
      "e2e": "ng e2e",
      "e2e:ci": "ng e2e -c protractor.conf.ci.js",
      "ci": "npm run lint:ci && npm run test:ci && npm run e2e:ci && npm run build:prod"
    },
  ```

1. To run any of these commands you run `npm run` and then the name of the script.  For example, below we are running the lint:ci script.

  ```bash
  npm run lint:ci
  ```