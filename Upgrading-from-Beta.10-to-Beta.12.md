We changed the build system between beta.10 and beta.12, from SystemJS to Webpack. And with it comes a lot of benefits. To take advantage of these, your app built with the old beta will need to migrate.

This page documents the steps to follow to migrate your old application to using the newest beta.

# Steps to Migrate

This guide assume your application is using SystemJS created with the `beta.10` and is up to date to >= Angular `RC6`. Also, make sure you committed everything from your project to Git.

1. Upgrade to the latest CLI globally:

    ```bash
    npm install -g angular-cli@latest
    ```

1. Create a new migration project:

    ```bash
    ng new migration-project
    ```

1. Backup the new `src/` to a different folder. We need those files later on.

    ```bash
    mv src/ src.webpacktemplate/
    ```

1. Replace the `src/` folder with your application's `src/` folder.
 
    ```bash
    mv ${OLD_PATH}/src src
    ```

1. Delete files that are not needed anymore.

    ```bash
    rm src/system-config.ts
    rm src/typings.d.ts
    ```

1. Copy files that are needed from a new project.

    ```bash
    cp src.webpacktemplate/polyfills.ts src/
    cp src.webpacktemplate/styles.css src/
    cp src.webpacktemplate/test.ts src/
    cp src.webpacktemplate/tsconfig.json src/
    cp src.webpacktemplate/typings.d.ts src/
    ```

1. In most cases, you can override your `src/main.ts` with the one in `src.webpacktemplate/main.ts`, but you might want to be careful if you have custom modifications to it.

1. In most cases, you can override your `src/index.html` with the one in `src.webpacktemplate/index.html`, but you might want to be careful if you have custom modifications to it.

1. Environments are now selected in the `angular-cli.json`. You need to edit that file, and change the files it points to in `apps[0].environment`.

1. Install npm dependencies that you were using. These may include (but not limited to):
   * Angular Material 2 (need HammerJS typings)
   * Angularfire2
   * Bootstrap
   * Firebase
   * jQuery
   * Moment
   * ...

    ```bash
    npm install --save ${LIBRARY}
    ```

    These libraries might have typings necessary, which you can install using:

    ```bash
    npm install --save-dev @types/${LIBRARY}
    ```

    Remember to copy any configuration or documentation files you have. For example, you might have a `firebase.json` file in the root of your repo. Don't forget your `LICENSE` and `README.md` file!

1. Remove all mention of `moduleId: module.id`. In webpack, `module.id` is a number but Angular expect a string.

1. Copy over your assets directory. Assets are now part of the app and not in the root of your repo.

    ```bash
    cp -R ${OLD_PATH}/public/ src/assets/
    ```

    Make sure to also remap your assets in your code. The new assets are served from `/assets/`.


1. Finally, **if you're using SASS or LESS**, you need to rename your `styleUrls` in all your files. Webpack understands LESS and SASS so you can use `styleUrls: ['my-component.scss']` in your component and it will be transcompiled automatically.

1. After all this, make sure you don't need anything else from the `src.webpacktemplate/` directory, try to `ng build`. If everything works, chances are you're good to go. Delete the `src.webpacktemplate/` directory.

1. Time to replace the git folder so you don't lose your history. Delete the `.git/` file in the new migration project. Then copy over your old `.git/` folder to replace it.

    ```bash
    rm -rf .git/
    cp -R ${OLD_PATH}/.git .
    ```

1. Go ahead and `ng serve` your app, then look at the resulting website. Adjust and adapt your code according to errors.
