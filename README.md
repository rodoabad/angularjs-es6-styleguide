# AngularJS ES6 Styleguide

This styleguide is another take on how to write AngularJS together with ESLint and ES6.

## Table of Contents

1. [Whitespace is FREE](#whitespace-is-free)
2. [Spaces, tabs, and indentation](#spaces-tabs-and-indentation)
3. [import and export](#import-and-export)
4. [const, let, and var](#const-let-and-var)
5. [Methods and chaining](#methods-and-chaining)
6. [Functions](#functions)
7. [Modules](#modules)
8. [Routes](#routes)
9. [Controllers](#controllers)
10. [Factories and Services](#factories-and-services)
11. [Directives](#directives)

## Whitespace is FREE

I cannot stress this enough. Adding whistespace is free and it makes your code easier to follow since you can now start grouping snippets of your code into their own mini-blocks.

## Spaces, tabs, and indentation

- Use spaces instead of tabs.
- Use **2** spaces for your indentation.
 
*Why?* Tab spacing differs on IDEs and text editors while spaces do not. By using spaces we eliminate that inconsistency.

## import and export

- Third party imports e.g. `node_modules` should be at the top-most level of your file followed by local imports separated by a whitespace.
- Constructors must use TitleCase i.e. `import MyService from './my-service'`.
- There should be a whitespace between your imports and the rest of your code.

```javascript
// Recommended
import angular from 'angular';
import uiRouter from 'angular-ui-router';

import MyService from './my-service';

// Rest of the code
```

## const and let

- `const` and `let` declarations must be on the same line as the keyword.
- `const` declarations should always be higher than `let` declarations and each group should be separated by a whitespace.
- `var` has no place in ES6.
- A whitespace should separate your declarations from the rest of your code.

```javascript
// Recommended

const users = UserSvc.getUsers();

let currentUserCount = 0;

// Rest of the code
```

```javascript
// Avoid

const
  users = UserSvc.getUsers();
  
let
  currentUserCount = 0;

// Rest of the code
```

```javascript
// Recommended

const admins = AdminSvc.getAdmins(),
  users = UserSvc.getUsers();
  
let currentAdminAcount = 0;
  currentUserCount = 0;

// Rest of the code
```

```javascript
// Avoid

const
  admins = AdminSvc.getAdmins(),
  users = UserSvc.getUsers();
  
let 
  currentAdminAcount = 0;
  currentUserCount = 0;

// Rest of the code
```

Single line declarations should be grouped with similar single line declarations while multi-line declarations should be in their own group. Each group must be separated by a whitespace.

```javascript
// Recommended

const maxUsers = 100;
  
const defaultGroups = [
    admin,
    manager,
    user
  ];

// Rest of the code
```

```javascript
// Avoid

const maxUsers = 100,
  defaultGroups = [
  admin,
  manager,
  user
];

// Rest of the code
```

## Methods and chaining

Single method calls must be written in a single line.
 
```javascript
// Recommended

angular.module('app', []);

// Rest of the code
```

Chained methods must be in a new line (per method). This provides a clear understanding of what's going on.

```javascript
// Recommended

angular
  .module('app')
  .controller('MainCtrl', MainCtrl)
  .directive('mainDirective', mainDirective);

// Rest of the code
```

## Functions

There should be a space before and after the function declaration and before and after you close that function.

```javascript
// Recommended

getTotal(key, items) {

  return items.reduce((sum, item) => sum + item[key], 0);

}

// Rest of the code
```

```javascript
// Avoid

getTotal(key, items) {
  return items.reduce((sum, item) => sum + item[key], 0);
}

// Rest of the code
```

```javascript
// Avoid

getTotal(key, items) {

  return items.reduce((sum, item) => sum + item[key], 0);
}

// Rest of the code
```

```javascript
// Avoid

getTotal(key, items) {
  return items.reduce((sum, item) => sum + item[key], 0);
  
}

// Rest of the code
```

### Naming Convention

Functions that will handle actions should be considered as events and therefore should be prefixed with `on`.

```javascript
// Recommended

function onUserEdit(name) {

  // Block code goes here

}

// Rest of the code
```

```javascript
// Avoid

function userEdit(name) {

  // Block code goes here

}

// Rest of the code
```

## Modules

### Declaration

Declare modules without a variable. Since we only use one component per file, there is no need to use a variable.

```javascript
// Recommended

angular.module('app', []);

// Rest of the code
```

```javascript
// Avoid

const app = angular.module('app', []);

// Rest of the code
```

### Naming Convention

Large applications typically has a lot of views that do different things. Naming your module per view allows you to separate your components depending on where they are being used rather than what they do. By doing this you can then have independent modules that you can easily extract into another repository if it gets too big living in your current repository.

*Assume your main application is called `app` and it has two separate views called `admin` and `user`.*

- Use dot notation to separate your views and subviews.
- Use a named array for your dependencies. This keeps your angular code lean.

```javascript
// Recommended
import angular from 'angular';

import admin from './views/admin';
import user from './views/user';

const dependencies = [
  admin,
  user
];

angular.module('app', dependencies);

// Rest of the code
```

```javascript
// Avoid
import angular from 'angular';

import admin from './views/admin';
import user from './views/user';

angular.module('app', [
  admin,
  user
]);

// Rest of the code
```

## Controllers

### ControllerAs syntax

Use **controllerAs** syntax every time.

*Why?* This ultimately helps you avoid using `$scope` when you bind things to Angular.

*Why?* This also helps you avoid name collisions and help keep your controllers tidy.

### ng-controller

Do not use `ng-controller` in your HTML files. Either declare your controller and controllerAs in your route or in your [directives](#directives).

```html
<!-- Avoid -->

<div ng-controller="MainCtrl as vm">

  <!-- Code goes here -->
  
</div>
```

#### Naming convention

Controllers should be in TitleCase and suffixed with `Ctrl`.

*Why?* This makes it easy to spot when you have a very large application. Having to use `Ctrl` instead of `Controller` also makes it easy on the eyes when you are looking for it.

```javascript
// Recommended

angular
  .module('app')
  .controller('MainCtrl', [
    MainCtrl
  ]);
```

```javascript
// Avoid

angular
  .module('app')
  .controller('mainCtrl', [
    mainCtrl
  ]);
```

```javascript
// Avoid

angular
  .module('app')
  .controller('main', [
    main
  ]);
```

```javascript
// Avoid

angular
  .module('app')
  .controller('MainController', [
    MainController
  ]);
```

#### Boilerplate

```javascript
// Recommended

import angular from 'angular';

class MainCtrl {

  /* @ngInject */
  constructor() {

    this.data = data;

  }

}

angular
  .module('app')
  .controller('MainCtrl', MainCtrl);

```


## Directives

```javascript
// Boilerplate

import template from './index.html';

function mainDirective() {
  return {
    restrict: 'E',
    template: template
  };
}

export default angular
  .module('app.mainDirective', [])
  .directive('mainDirective', mainDirective)
  .name;
```

## Unit Testing

Use the **Arrange-Act-Assert** pattern when arranging and formatting code in your unit tests.

### Before Each

### Dependency Injections

Dependency injections must use double underscore notation and must be the same name as their counterpart variables. i.e. `$rootScope` will be `_$rootScope_`.

*Why?* This helps separate your variables between your dependencies.

Each dependency must be in a new line if there is more than one dependency being injected.

*Why?* This makes it a lot easier to follow when you have more than 2 dependencies.

```javascript
      inject((
        _$location_,
        _$q_,
        _$rootScope_,
        _$state_
      ) => {});
```

#Legacy

## IIFE, strict mode, and window

- Every single file must be wrapped in an IIFE (Immediately-Invoked Function Expression) and have strict mode enabled. This prevents variables and function declarations from leaking outside of your current scope.
- Global variables like `angular` should be localized.

```javascript
(() => {

  'use strict';

  const angular = window.angular;
  
})();
```

## Legacy Styles

1. [IIFE, strict mode, and window](#iife-strict-mode-and-window)

# License

Copyright (c) 2015 Rodo Abad

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
