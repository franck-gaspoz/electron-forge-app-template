# electron-test-project

___

## setup a sample project

install/update nodejs (windows: download nodejs last version [>=20])
example: <https://nodejs.org/dist/v20.0.0/node-v20.0.0-x64.msi>

``` shell
cd C:\Program Files\nodejs

corepack enable

@rem update global yarn version
corepack prepare yarn@stable --activate

@rem update yarn
yarn set version stable

cd {projetFolderParentFolder}
yarn create electron-app my-app --template=webpack

npm install electron --save-dev

yarn start

```

___

## setup debug in vscode

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
