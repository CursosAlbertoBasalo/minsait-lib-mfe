# Minsait Libraries

> [Repositorios Cursos](https://github.com/CursosAlbertoBasalo/minsait-lib-mfe)

Incluye este guión de comandos y los diagramas de arquitectura del proyecto.

## Applications

### Ng app

```bash
ng new mst-ng-app -s -t --ssr=false --style=css
cd mst-ng-app
npm link @mst/ui --save
```

- In order to use linked libraries

```json
{
  "projects": {
    "mst-ng-app": {
      "architect": {
        "build": {
          "options": {
            "preserveSymlinks": true
          }
        }
      }
    }
  },
  "cli": {
    "analytics": false,
    "cache": {
      "enabled": false
    }
  }
}
```

```bash
npm start
```

### Non Angular ecosystem

```bash
mkdir mst-js-app
cd mst-js-app
npm init -y
git init
# Add .gitignore
# Create an HTML file
npm link @mst/wbc --save
# "start": "npx http-server ./ -p 8080 "
npm start
```

## UI workspace

### mst-ws-ui workspace

```bash
ng new mst-ws-ui --no-create-application
cd mst-ws-ui
```

### mst-ui library

```bash
ng g lib mst-ui --prefix=mst-ui
ng config projects.mst-ui.schematics.@schematics/angular:component.changeDetection "OnPush"
ng config projects.mst-ui.schematics.@schematics/angular:component.flat true
ng config projects.mst-ui.schematics.@schematics/angular:component.inlineTemplate true
ng config projects.mst-ui.schematics.@schematics/angular:component.inlineStyle false
ng config projects.mst-ui.schematics.@schematics/angular:component.style "none"
ng g c location
ng g c date
```

### mst-ui-dev application

```bash
ng g app mst-ui-dev --routing=false --ssr=false --style=css -S -s -t
# import relative source
# "start": "ng serve mst-ui-dev",
npm start
```

### npm publish (or link) for Angular ecosystem

#### Version control

- At workspace package.json

```bash
npm i -D standard-version
```

- At mst-ui package.json

```json
{
  "name": "@mst/ui",
  "description": "A library with Angular UI components, pipes, and directives for Minsait projects",
  "version": "0.0.1",
  "scripts": {
    "release": "standard-version"
  },
  "peerDependencies": {
    "@angular/common": "^18.0.0",
    "@angular/core": "^18.0.0"
  },
  "dependencies": {
    "tslib": "^2.3.0"
  },
  "sideEffects": false
}
```

#### Build and link

- At workspace package.json

```bash
# "build": "ng build mst-ui --configuration production",
npm run build
# "prepublish": "npm run build && cd ./projects/mst-ui && npm run release",
# "publish": "cd ./dist/mst-ui && npm link",
# "postpublish": "git push --follow-tags origin main",
npm publish
# list global npm links
npm ls -g --depth=0
```

### mst-ui-wbc application for non Angular ecosystem

```bash
ng g app mst-ui-wbc --routing=false --ssr=false --style=css -S -s -t
npm i @angular/elements
```

- At public folder of mst-ui-wbc

```json
{
  "name": "@mst/wbc",
  "description": "Web Component library for Minsait projects",
  "version": "0.0.1",
  "scripts": {
    "release": "standard-version"
  },
  "main": "main.js",
  "files": ["main.js", "styles.css"]
}
```

#### Pack and Publish

```bash
# "build:wbc": "ng build mst-wbc --configuration production ",
# "prepack": "npm run build:wbc && cd ./projects/mst-ui-wbc/public && npm run release",
# "pack": "cd ./dist/mst-ui-wbc/browser && npm link",
# "postpack": "git push --follow-tags origin main",
npm run pack
# list global npm links
npm ls -g --depth=0
```

## Other Libraries workspaces

### mst-ws-srv workspace

#### mst-srv library generation

```bash
ng new mst-ws-srv --no-create-application
cd mst-ws-srv
ng g lib mst-srv
ng g s logger
ng g s crud-repository
```

#### Build and publish

```json
{
  "name": "@mst/srv",
  "description": "A library with services for Minsait projects",
  "version": "0.0.1",
  "scripts": {
    "release": "standard-version"
  },
  "peerDependencies": {
    "@angular/common": "^18.0.0",
    "@angular/core": "^18.0.0"
  },
  "dependencies": {
    "tslib": "^2.3.0"
  },
  "sideEffects": false
}
```

```bash
# "build": "ng build --configuration production",
npm run build
# "prepublish": "cd ./projects/mst-srv && npm run release ",
# "publish": "npm run build && cd ./dist/mst-srv && npm link",
# "postpublish": "git push --follow-tags origin main"
npm run publish
```

> Tokens for configure the library in the Angular application

### mst-ws-core workspace

#### mst-core library generation

```bash
ng new mst-ws-core --no-create-application
cd mst-ws-core
ng g lib mst-core
ng g interceptor metrics
ng g class error-service
```

#### Build and publish

```json
{
  "name": "@mst/core",
  "description": "A library with core services for Minsait projects",
  "version": "0.0.1",
  "scripts": {
    "release": "standard-version"
  },
  "peerDependencies": {
    "@angular/common": "^18.0.0",
    "@angular/core": "^18.0.0"
  },
  "dependencies": {
    "tslib": "^2.3.0"
  },
  "sideEffects": false
}
```

```bash
# "build": "ng build --configuration production",
npm run build
# "prepublish": "cd ./projects/mst-core && npm run release ",
# "publish": "npm run build && cd ./dist/mst-core && npm link",
# "postpublish": "git push --follow-tags origin main"
npm run publish
```

> Warning: Beware of the library dependencies

> ToDo: Security: Add an Auth library or include the feature in mst-core

### Non Angular ecosystem Libraries

#### mst-ws-domain workspace

```bash
mkdir mst-ws-domain
cd mst-ws-domain
```

#### mst-domain library generation using vite

```bash
npm create vite@latest mst-domain --template vanilla-ts
cd mst-domain
npm install
npm i -D standard-version
```

> Remove everything but the src/main and the vite files

> Add vite.config.ts

```ts
import { defineConfig } from "vite";
export default defineConfig({
  build: {
    lib: {
      entry: "src/main.ts",
      name: "domain",
      fileName: "domain",
    },
  },
});
```

> Add public/package.json

```json
{
  "name": "@mst/domain",
  "description": "A library with domain services for Minsait projects",
  "version": "0.0.1",
  "scripts": {
    "release": "standard-version"
  },
  "peerDependencies": {
    "tslib": "^2.3.0"
  },
  "sideEffects": false
}
```

#### Build and link

```bash
# "prebuild": "tsc",
# "build": "vite build",
# "prepublish": "cd ./public && npm run release ",
# "publish": "npm run build && cd ./dist && npm link",
# "postpublish": "git push --follow-tags origin main"
npm run publish
```
