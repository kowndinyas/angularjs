# 3rd party lib installation

Examples of how to install 3rd party libraries.

Table of contents:
- [Adding moment.js library to your project](#adding-momentjs-library-to-your-project)
- [Adding material2 to your project](#adding-material2-to-your-project)

## Adding moment.js library to your project

### 1. Install moment.js via npm

```
npm install moment --save
```

### 2. Install typings for moment.js library

```
typings install moment moment-node --ambient --save
```

### 3. Add moment.js to angular-cli-build.js file to vendorNpmFiles array

This is required so the build system will pick up the file. After setup the `angular-cli-build.js` should look like this:

```js
var Angular2App = require('angular-cli/lib/broccoli/angular2-app');

module.exports = function(defaults) {
  var app = new Angular2App(defaults, {
    vendorNpmFiles: ['moment/moment.js']
  });
  return app.toTree();
};
```

### 4. Configure SystemJS mappings to know where to look for moment.js

SystemJS configuration is located in `index.html` and after the configuration is done should look something like:

```html
<script>
  System.config({
    packages: {
      app: {
        format: 'register',
        defaultExtension: 'js'
      }
    },
    map: {
      'moment': 'vendor/moment/moment.js'
    }
  });
  System.import('app.js').then(null, console.error.bind(console));
</script>
```

### 5. Importing and using moment.js library in your project source files

Import moment.js library in your source `.ts` files like this:

```ts
import * as moment_ from 'moment';
const moment: moment.MomentStatic = (<any>moment_)['default'] || moment_;
```

If you followed the steps correctly you should now have moment.js library working in your project. Enjoy!

___

## Adding material2 to your project

### 1. Install material2 core

```
npm install @angular2-material/core --save
```

### 2. Install material2 package you'll use

```
npm install @angular2-material/checkbox --save
```

Current available packages for material2 are
- button
- card
- checkbox
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
  var app = new Angular2App(defaults, {
    vendorNpmFiles: ['@angular2-material/**/*.js']
  });
  return app.toTree();
};
```

This will make files available in the `dist/` folder.

### 4. Set up your SystemJS configuration

SystemJS configuration is located in `index.html` and here's an example of how to configure it:

```html
<script>
  System.config({
    map: {
      '@angular2-material': 'vendor/@angular2-material'
    },
    packages: {
      app: {
        format: 'register',
        defaultExtension: 'js'
      },
      '@angular2-material': {
        map: {
          './button': './button/button.js',
          './card': './card/card.js',
          './checkbox': './checkbox/checkbox.js',
          './input': './input/input.js',
          './progress-circle': './progress-circle/progress-circle.js',
          './sidenav': './sidenav/sidenav.js',
          './toolbar': './toolbar/toolbar.js',
        }
      }
    }
  });
  System.import('app.js').then(null, console.error.bind(console));
</script>
```

### 5. Example of use material2 component

Example of use material2 component:

```ts
import {Component} from 'angular2/core';
import {MdCheckbox} from '@angular2-material/checkbox';

@Component({
  selector: 'my-component',
  template: `<md-checkbox></md-checkbox>`,
  directives: [MdCheckbox]
})
```

Congratulations, you now have material2 components available to use in your project. Enjoy!
