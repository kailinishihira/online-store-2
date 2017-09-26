# Angular Cheatsheet

### Global Commands - setting up your computer for the first time to work with Angular CLI

Install Angular CLI
`npm install -g @angular/cli@1.0.0`

Install Typescript
`npm list -g typescript`

Install Bower
`npm install bower -g`

### Project setup

Create new Angular App
`ng new project-name`

In `src/main.ts` add polyfills to imports
`import './polyfills.ts';`

Initialize Bower in project root
`bower init`

Add `bower_components` to `.gitignore`
```
...
# dependencies
/node_modules
/bower_components
...
```

Install Bootstrap dependency in Bower
`bower install bootstrap --save`

In `.angular-cli.json` add Bootstrap style
```
...
"apps": [
    {
      ...
      ],
      ...
      "styles": [
        "styles.css",
        "../bower_components/bootstrap/dist/css/bootstrap.css"
      ],
...
```
Serve app in browser
`ng serve`

Use Angular build-in linter
`ng lint`

Create new component
`ng g component component-name`

Create new pipe
`ng g pipe pipe-name`

Create new class
`ng g class class-name.model`

Create `app.routing.ts` file in `app` and add below. Also change `ComponentName` to actual name of component. This sets up your homepage view ie splash page
```
import { ComponentName} from './component-name/component-name.component';
import { ModuleWithProviders }  from '@angular/core';
import { Routes, RouterModule } from '@angular/router';

const appRoutes: Routes = [
  {
    path: '',
    component: ComponentName
  }
];

export const routing: ModuleWithProviders = RouterModule.forRoot(appRoutes);

```

Add routing `import` and new component `import` to `app.module.ts`

```
...
import { ComponentName} from './component-name/component-name.component';
import { routing } from './app.routing';
...
```

Add `routing` constant to `app.module.ts`

```
...
  imports: [
    BrowserModule,
    FormsModule,
    HttpModule,
    routing
  ],
...
```

Add `<router-outlet` to `app.component.html`

```
<div class="container">
  <h1>{{title}}</h1>
  <router-outlet></router-outlet>
</div>
```

Change the `title` property in `AppComponent` class in `app.component.ts`

```
...
export class AppComponent {
  title = 'Site Name';
}
```

### Creating multiple pages

Add `path` of multiple page to `app.routing.ts`
```
import { ModuleWithProviders } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';
import { WelcomeComponent } from './welcome/welcome.component';
import { AboutComponent }   from './about/about.component';

const appRoutes: Routes = [
  {
     path: '',
     component: WelcomeComponent
   },
  {
    path: 'about',
    component: AboutComponent
  }
 ];

export const routing: ModuleWithProviders = RouterModule.forRoot(appRoutes);
```

Insert a `routerLink` into `app.component.html`
```
<nav class="navbar navbar-default">
  <div class="container-fluid">
    <div class="navbar-header">
      <a class="navbar-brand" routerLink="">Epicodus Tunes</a>
    </div>
    <ul class="nav navbar-nav navbar-right">
      <li><a routerLink="about">About</a></li>
    </ul>
  </div>
</nav>

<div class="container">
  <h1>{{title}}</h1>
  <router-outlet></router-outlet>
</div>
```

### Dynamic Routing







##Create firebase
`npm install angularfire2@4.0.0-rc.0 firebase --save`

In tsconfig.json add `"types": [ "firebase" ]` to the very end of the file.
```
{
  "compileOnSave": false,
  "compilerOptions": {
    "outDir": "./dist/out-tsc",
    "baseUrl": "src",
    "sourceMap": true,
    "declaration": false,
    "moduleResolution": "node",
    "emitDecoratorMetadata": true,
    "experimentalDecorators": true,
    "target": "es5",
    "typeRoots": [
      "node_modules/@types"
    ],
    "lib": [
      "es2016",
      "dom"
    ],
    "types": [ "firebase" ]
  }
}
```
### Add Firebase credentials
Create an account with [Firebase](https://firebase.google.com/).
Create a new file in src/app directory `src/app/api-keys.ts` and paste the code (replace with your credentials):
```
export var masterFirebaseConfig = {
    apiKey: "xxxx",
    authDomain: "xxxx.firebaseapp.com",
    databaseURL: "https://xxxx.firebaseio.com",
    storageBucket: "xxxx.appspot.com",
    messagingSenderId: "xxxx"
  };
```
### Add file to .gitignore.
```
#Firebase credentials
/src/app/api-keys.ts
```

### Import modules and export firebaseConfig into `app.module.ts`
```
import { masterFirebaseConfig } from './api-keys';
import { AngularFireModule } from 'angularfire2';
import { AngularFireDatabaseModule } from 'angularfire2/database';

export const firebaseConfig = {
  apiKey: masterFirebaseConfig.apiKey,
  authDomain: masterFirebaseConfig.authDomain,
  databaseURL: masterFirebaseConfig.databaseURL,
  storageBucket: masterFirebaseConfig.storageBucket
};
```

### Update `imports` section in `app.module.ts`.
```
imports: [
    BrowserModule,
    FormsModule,
    HttpModule,
    routing,
    AngularFireModule.initializeApp(firebaseConfig),
    AngularFireDatabaseModule
  ]
  ```

### Update Firebase rules to be "true" in the Firebase database.
Database => Rules
```
{
  "rules": {
    ".read": "true",
    ".write": "true"
  }
}
```

### Install promise-polyfill if you encounter error: Can't resolve 'promise-polyfill'
`npm install promise-polyfill --save-exact`

#### If you would like to upload an existing local json file to the Firebase database, select `Import JSON` from the database menu and select file to import.

### Retrieving Data from Firebase (you may also retrieve data from a component directly).
Import dependencies into your app service or component file and declare the class property to FirebaseListObservable<any[]> type.
`import { AngularFireDatabase, FirebaseListObservable } from 'angularfire2/database';`

example:
```
@Injectable()
export class AlbumService {
  albums: FirebaseListObservable<any[]>;
```

# OnlineStore

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 1.0.0.

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive/pipe/service/class/module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory. Use the `-prod` flag for a production build.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via [Protractor](http://www.protractortest.org/).
Before running the tests make sure you are serving the app via `ng serve`.

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI README](https://github.com/angular/angular-cli/blob/master/README.md).
