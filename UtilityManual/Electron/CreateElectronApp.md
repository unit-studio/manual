# Electron 新建项目

查看 [打造你的第一个 Electron 应用](https://electronjs.org/docs/tutorial/first-app#%E6%89%93%E9%80%A0%E4%BD%A0%E7%9A%84%E7%AC%AC%E4%B8%80%E4%B8%AA-electron-%E5%BA%94%E7%94%A8)

## 1. 创建node项目

```shell
mkdir ElectronWorkspace && cd ElectronWorkspace
npm init
```

查看项目配置

```
{
  "name": "your-app",
  "version": "0.1.0",
  "main": "main.js",
  "scripts": {
    "start": "electron ."
  }
}
```

> 如果报错 `TypeError: Cannot read property 'on' of undefined`
> 查看 [Electron - “Cannot read property 'on' of undefined”](https://stackoverflow.com/questions/50166100/electron-cannot-read-property-on-of-undefined-tried-reinstalling)
>> You are probably trying to run your application like a node app with:
>> `$ node index.js`
>> The electron file is a binary file, not a JavaScript file, when you require it an run with node there will be no object to call electron.app, so it parses for null and cannot have an property. As in the getting started documento of Electron.JS you must run the application like this:
>> Change your package.json script session adding start:
>> ```json
>> {
>>     "scripts": {
>>         "start": "electron ."
>>     }
>> }
>> ```
>> Now run:
>> ```shell
>> $ npm start
>> ```

## 2. 引入Electron

```shell
npm install --save-dev electron
```

## 3. 开发一个简易的Electron项目

修改 main.js 文件:

```
const { app, BrowserWindow } = require('electron')

// 保持对window对象的全局引用，如果不这么做的话，当JavaScript对象被
// 垃圾回收的时候，window对象将会自动的关闭
let win

function createWindow () {
  // 创建浏览器窗口。
  win = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      nodeIntegration: true
    }
  })

  // 加载index.html文件
  win.loadFile('index.html')

  // 打开开发者工具
  win.webContents.openDevTools()

  // 当 window 被关闭，这个事件会被触发。
  win.on('closed', () => {
    // 取消引用 window 对象，如果你的应用支持多窗口的话，
    // 通常会把多个 window 对象存放在一个数组里面，
    // 与此同时，你应该删除相应的元素。
    win = null
  })
}

// Electron 会在初始化后并准备
// 创建浏览器窗口时，调用这个函数。
// 部分 API 在 ready 事件触发后才能使用。
app.on('ready', createWindow)

// 当全部窗口关闭时退出。
app.on('window-all-closed', () => {
  // 在 macOS 上，除非用户用 Cmd + Q 确定地退出，
  // 否则绝大部分应用及其菜单栏会保持激活。
  if (process.platform !== 'darwin') {
    app.quit()
  }
})

app.on('activate', () => {
  // 在macOS上，当单击dock图标并且没有其他窗口打开时，
  // 通常在应用程序中重新创建一个窗口。
  if (win === null) {
    createWindow()
  }
})

// 在这个文件中，你可以续写应用剩下主进程代码。
// 也可以拆分成几个文件，然后用 require 导入。
```

修改 index.html 文件:

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>Hello World!</title>
  </head>
  <body>
    <h1>Hello World!</h1>
    We are using node <script>document.write(process.versions.node)</script>,
    Chrome <script>document.write(process.versions.chrome)</script>,
    and Electron <script>document.write(process.versions.electron)</script>.
  </body>
</html>
```

## 4. 启动项目

在创建并初始化完成 main.js、 index.html和package.json之后，您就可以在当前工程的根目录执行 npm start 命令来启动刚刚编写好的Electron程序了。

```shell
npm start
```
