
# Storybook

This page includes stories to create Angular CLI apps.

**Please note that not all stories are currently implemented.**

## App Creation
```bash
# Create an app
ng new my-todo-app

# Generate a TODO component
ng generate component todo

# Serve the app
ng serve
```

## App Creation Using Template
```bash
ng new my-todo-app --template=simple-todo
ng serve
```

#### Using A Template Library
```bash
ng new my-todo-app
# Could be `ng use` as well.
ng install complex-todo-addon
ng generate todo routes/+todo
```

## Thirdparty Installation
```bash
ng new my-todo-app
ng install sass
```