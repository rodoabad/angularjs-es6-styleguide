# AngularJS ES6 Styleguide

This styleguide is another take on how to write AngularJS together with ESLint and ES6.

## Table of Contents

1. [Spaces, tabs, and indentation](#spaces-tabs-and-indentation)
2. [import and export](#import-and-export)
3. [const, let, and var](#const-let-and-var)
4. [Methods and chaining](#methods-and-chaining)
5. [Functions](#functions)
6. [Modules](#modules)
7. [Routes](#routes)
8. [Controllers](#controllers)
9. [Factories and Services](#factories-and-services)
10. [Directives](#directives)
11. 

## Legacy Styles

1. [IIFE, strict mode, and window](#iife-strict-mode-and-window)

## Spaces, tabs, and indentation

- Use spaces instead of tabs.
- Use 2 spaces for your indentation.
 
*Why?* Tab spacing differs on IDEs and text editors while spaces do not. By using spaces we eliminate that inconsistency.

## import and export

- Global imports e.g. `node_modules` should be at the top most level of your file. Local imports should then be after your global imports
- Constructors must use TitleCase i.e. `import MyServer from './my-server'`.

```javascript
// Recommended
import angular from 'angular';
import uiRouter from 'angular-ui-router';

import MyLocalSvc from './my-local-svc';

// ...
```

## const, let, and var

Declarations must be on the same line as the keyword.

```javascript
// Recommended

let users = UserSvc.getUsers();
```

```javascript
// Avoid

let
  users = UserSvc.getUsers();
```

```javascript
// Recommended

let admins = AdminSvc.getAdmins(),
  users = UserSvc.getUsers();
```

```javascript
// Avoid

let
  admins = AdminSvc.getAdmins(),
  users = UserSvc.getUsers();
```

Single line declarations should be grouped with other single line declarations while multi-line declarations should be in their own group.

```javascript
// Recommended

const maxUsers = 100;
  
const defaultGroups = [
    admin,
    manager,
    user
  ];
```

```javascript
// Avoid

const maxUsers = 100,
  defaultGroups = [
  admin,
  manager,
  user
];
```

## Methods and chaining

Single method calls must be written in a single line.
 
```javascript
// Recommended

angular.module('app', [])
```

Chained methods must be in a new line (per method). This provides a clear understanding of what's going on.

```javascript
// Recommended

angular
  .module('app')
  .controller('MainCtrl', [
    MainCtrl
  ]);
```

## Functions

There should be a space before and after the function declaration and before and after you close that function.

```javascript
// Recommended

getTotal(key, items) {

  return items.reduce((sum, item) => sum + item[key], 0);

}
```

```javascript
// Avoid

getTotal(key, items) {
  return items.reduce((sum, item) => sum + item[key], 0);
}
```

```javascript
// Avoid

getTotal(key, items) {

  return items.reduce((sum, item) => sum + item[key], 0);
}
```

```javascript
// Avoid

getTotal(key, items) {
  return items.reduce((sum, item) => sum + item[key], 0);
  
}
```

### Naming Convention

Functions that will handle actions should be considered as events and therefore should be prefixed with `on`.

```javascript
// Recommended

function onUserEdit(name) {

  // Code goes here

}
```

```javascript
// Avoid

function userEdit(name) {

  // Code goes here

}
```

## Modules

Declare modules without a variable.

*Why?* Since we only use one component per file, there is no need to use a variable.

```javascript
// Recommended

angular.module('app', []);
```

```javascript
// Avoid

const app = angular.module('app', []);
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

(() => {

  'use strict';

  const angular = window.angular;

  class MainCtrl {

    constructor() {

      this.data = data;

    }

  }

  angular
    .module('app')
    .controller('MainCtrl', [
      MainCtrl
    ]);

})();
```


## Directives

```javascript
// Boilerplate

(() => {

  'use strict';

  const angular = window.angular;

  function mainDirective(
    MainDirectiveSvc
  ) {

    function link() {

      // Code goes here

    }

    return {
      link: link,
      restrict: 'E',
      templateUrl: 'main-directive.html'
    };

  }

  angular
    .module('app')
    .directive('mainDirective', [
      'MainDirectiveSvc',
      mainDirective
    ]);

})();
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

# License

Copyright (c) 2015 Rodo Abad

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
