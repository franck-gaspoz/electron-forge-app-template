# Electron Forge application template

___

This project is a NodeJs Electron Forge TypeScript application that actually displays a simple web page, provided by the electron application. Everything is already configured and ready to run. It is delivered in a template repository

usage:

``` shell
// clone the repo
git clone https://github.com/franck-gaspoz/electron-forge-app-template.git

// run the application
yarn start
```

___

## Development notes
### How to reconstruct the project from void

install/update nodejs (windows: download nodejs last version [>=20])
example: <https://nodejs.org/dist/v20.0.0/node-v20.0.0-x64.msi>

``` shell
// from the shell running with admin privileges

cd C:\Program Files\nodejs

corepack enable

@rem update global yarn version
corepack prepare yarn@stable --activate

@rem update yarn
yarn set version stable

cd {projetFolderParentFolder}
yarn create electron-app my-app --template=webpack-typescript

npm install electron --save-dev

yarn start

```

___

## Setup debug in vscode

This is a part of the application template.

``` json
{
  "version": "0.2.0",
  "compounds": [
    {
      "name": "Main + renderer",
      "configurations": ["Main", "Renderer"],
      "stopAll": true
    }
  ],
  "configurations": [
    {
      "name": "Renderer",
      "port": 9222,
      "request": "attach",
      "type": "chrome",
      "webRoot": "${workspaceFolder}"
    },
    {
      "name": "Main",
      "type": "node",
      "request": "launch",
      "cwd": "${workspaceFolder}",
      "runtimeExecutable": "${workspaceFolder}/node_modules/.bin/electron",
      "windows": {
        "runtimeExecutable": "${workspaceFolder}/node_modules/.bin/electron.cmd"
      },
      "args": [".", "--remote-debugging-port=9222"],
      "outputCapture": "std",
      "console": "integratedTerminal"
    }
  ]
}
```
