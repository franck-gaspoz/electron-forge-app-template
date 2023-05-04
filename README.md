# Electron Forge application template

___

![project illustration](https://raw.githubusercontent.com/franck-gaspoz/electron-forge-app-template/main/assets/Node%20JS%20Electron%20Forge%20sample%20app.png)

This project is a **Node.Js Electron Forge TypeScript** application that actually displays a simple web page, provided by the electron application. Everything is already configured and ready to run. It is delivered in a template repository

usage:

📝 command sequences for the shell (adapt to yours, here windows/dos)

**prepare and run**

``` shell

# clone the template repo

git clone https://github.com/franck-gaspoz/electron-forge-app-template.

cd electron-forge-app-template

# prepare and run the application

yarn install
yarn start
```

**develop &amp; debug**

``` shell
cd electron-forge-app-template
code .
```

**debug**

Run and Debug ▶️ Main + render

___

## Development notes
### How to reconstruct the project from void

install/update nodejs (for windows: download nodejs last version [>=20], for example: <https://nodejs.org/dist/v20.0.0/node-v20.0.0-x64.msi>)

📝 command sequence for the shell (adapt to yours, here windows/dos)

``` shell
# from the shell running with admin privileges

cd C:\Program Files\nodejs

corepack enable

# update global yarn version
corepack prepare yarn@stable --activate

# update yarn
yarn set version stable

cd {projetFolderParentFolder}
yarn create electron-app my-app --template=webpack-typescript

npm install electron --save-dev

# optional
#yarn start

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
