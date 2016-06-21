# 3rd party lib installation

Examples of how to install 3rd party libraries.

Table of contents:
- [Adding moment.js library to your project](#adding-momentjs-library-to-your-project)
- [Adding material2 to your project](#adding-material2-to-your-project)
- [Adding underscore library to your project](#adding-underscore-library-to-your-project)

## Adding moment.js library to your project

### 1. Install moment.js via npm

```bash
npm install moment --save
```

### 1a. **OPTIONAL** Install typings for library

Moment already includes typings, but not all libraries do. To add typings for a library, do the following:

```bash
typings install LIBRARY_NAME --global --save
```

### 2. Add moment.js to angular-cli-build.js file to vendorNpmFiles array

This is required so the build system will pick up the file. After setup the `angular-cli-build.js` should look like this:

```js
var Angular2App = require('angular-cli/lib/broccoli/angular2-app');

module.exports = function(defaults) {
  return new Angular2App(defaults, {
    vendorNpmFiles: [
      // ...
      'moment/moment.js'
    ]
  });
};
```

### 3. Configure SystemJS mappings to know where to look for moment.js

SystemJS configuration is located in `system-config.ts` and after the custom configuration is done the related section should look like:

```ts
/** Map relative paths to URLs. */
const map: any = {
  'moment': 'vendor/moment/moment.js'
};

/** User packages configuration. */
const packages: any = {
  'moment':{
    format: 'cjs'
  }
};
```

### 4. Importing and using moment.js library in your project source files

Import moment.js library in your source `.ts` files like this:

```ts
import * as moment from 'moment';
moment().format();
```

If you followed the steps correctly you should now have moment.js library working in your project. Enjoy!

___

## Adding material2 to your project

### 1. Install material2 core

```bash
npm install @angular2-material/core --save
```

### 2. Install material2 package you'll use

```bash
npm install @angular2-material/checkbox --save
```

Current available packages for material2 are
- button
- card
- checkbox
- icon
- input
- list
- progress-bar
- progress-circle
- radio
- sidenav
- toolbar

### 3. Include material2 into angular-cli-build.js

The `angular-cli-build.js` content after the setup should look like;

```js
var Angular2App = require('angular-cli/lib/broccoli/angular2-app');

module.exports = function(defaults) {
  return new Angular2App(defaults, {
    vendorNpmFiles: [
      '@angular2-material/**/*.js'
    ]
  });
};
```

This will make files available in the `dist/` folder.

### 4. Set up your SystemJS configuration

SystemJS configuration is located in `system-config.ts` and here's an example of how to configure it (custom section):

```ts
/** Map relative paths to URLs. */
const map: any = {
  '@angular2-material': 'vendor/@angular2-material'
};

/** User packages configuration. */
const packages: any = {
  '@angular2-material/core': {
    format: 'cjs',
    defaultExtension: 'js',
    main: 'core.js'
  },
  '@angular2-material/checkbox': {
    format: 'cjs',
    defaultExtension: 'js',
    main: 'checkbox.js'
  },
  // And so on...
};
```

### 5. Example of use material2 component

Example of use material2 component:

```ts
import { Component } from '@angular/core';
import { MdCheckbox } from '@angular2-material/checkbox';

@Component({
  selector: 'my-app',
  template: `<md-checkbox></md-checkbox>`,
  directives: [MdCheckbox]
})
export class AppComponent { }
```

Congratulations, you now have material2 components available to use in your project. Enjoy!

___

## Adding underscore library to your project

### 1. Install underscore via npm

```bash
npm install underscore --save
```

### 1a. Install typings for library

Underscore does not have typings installed unlike moment. To add typings for a library, do the following:

```bash
typings install underscore --global --save
```

### 2. Add underscore to angular-cli-build.js file to vendorNpmFiles array

This is required so the build system will pick up the file. After setup the `angular-cli-build.js` should look like this:

```js
var Angular2App = require('angular-cli/lib/broccoli/angular2-app');

module.exports = function(defaults) {
  return new Angular2App(defaults, {
    vendorNpmFiles: [
      // ...
      'underscore/underscore.js'
    ]
  });
};
```

### 3. Configure SystemJS mappings to know where to look for underscore

SystemJS configuration is located in `system-config.ts` and after the custom configuration is done the related section should look like:

```ts
/** Map relative paths to URLs. */
const map: any = {
  'underscore': 'vendor/underscore/underscore.js'
};

/** User packages configuration. */
const packages: any = {
  'underscore':{
    format: 'cjs'
  }
};
```

### 4. Importing and using underscore library in your project source files

Import moment.js library in your source `.ts` files like this:

```ts
import * as underscore from 'underscore';
_.each([1, 2, 3], alert);
```

If you followed the steps correctly you should now have underscore library working in your project. Enjoy!