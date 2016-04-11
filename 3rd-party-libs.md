# 3rd party lib installation

Examples of how to install 3rd party libraries.

*We are aware that this procedure is not user-friendly and it will be improved in the future.*

## Adding moment.js library to your project

### 1. Install moment.js via npm

```
npm install moment
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