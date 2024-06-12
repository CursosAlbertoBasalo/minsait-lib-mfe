# Minsait Libraries

> [Repositorios Cursos](https://github.com/CursosAlbertoBasalo/minsait-lib-mfe)

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

```bash
npm i -D standard-version
```

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

#### Build and publish

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
# "prepack": "npm run build:wbc && cd ./projects/mst-wbc && npm run release",
# "pack": "copyfiles projects/mst-wbc/package.json dist/mst-wbc/browser -f ",
# "postpack": "cd ./dist/mst-wbc/browser && npm link",
# list global npm links
npm ls -g --depth=0
```

## Applications

### Ng app

```bash
ng new mst-ng-app -s -t --ssr=false --style=css
cd mst-ng-app
npm link @mst/ui
```

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
# Create an HTML file
npm link @mst/wbc
# "start": "npx http-server ./ -p 8080 "
npm start
```
