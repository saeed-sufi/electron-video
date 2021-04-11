# electron-video
## First taste of electron

* `ffmpeg` is the most popular command line tool to work with video files. `fluent-ffmpeg` is the wrapper which makes it easier to work with `ffmpeg`.

* `app` object is responsible for runnig electron process on our machine.

* whenever we need to make a menu, first we need to make a menu template. It's an object or an array which is the structure of the menu.

* If you need to check what platform your app is running on, run `process.platform` on your index.js. If it's MacOS it will be equal to `darwin`. If it's windows, it's `win32`.

* when inside an object, you can use `IIFE` to decide what value to assign to a property of the object. In electron you need to use an IIFE for the `accelerator` property of a `submenu` object.

* If you need to check whether you are in development or production mode, check `process.env.NODE_ENV`. Possible values are `production, staging, development`

* In electron, whenever we close a window, we have to assign the window object to `null` so that the JS garbage collector would know that it can reclaim the memory which was occupied by the window. 

* In order to make your electron app more performant, consider applying the following rules: 
  * Bundle your code using webpack. `require` is an expensive operation. So, it's better to load only one js file.
  * Your app should be able to work offline. So, download everything you need for your app to run and include them in your app's bundle
  * Don't use polyfills. Electron has them all.
  * Use web workers and `requestidlecallback()` to avoid blocking the renderer process.
  * always prefer async modules. Avoid using synchronous IPC and `remote` module as much as possible. Make use of worker threads for CPU-heavy tasks.
  * load modules whenever you need them not at the top of your file. `require` comes with a module cache, so it runs faster next time it is called.
  * profiling the modules you use, is the best solution to improve your app performance. `node --cpu-prof --heap-prof -e "require('request')"`
* The `super` keyword is a reference to the parent class constructor. So, it has to take care of the parent's constructor arguments.

* If no variable is pointing toward the `new` instance of a class that you made, this new instance will be collected by the garbage collector. 


* communications between `main` and `renderer` processes:

![communications](https://github.com/saeed-sufi/electron-video/blob/master/ipcObjs.png)
* When the app window is not focused, chromium is going to assume that you dont care about your app and it starts to limit the resources used by the js on the app. This leads to your app starts throttling. In order to prevent such behaviour, we need o set `backgroundThrottling: false` in the `webPrefences` option of the BrowserWindow instance. 

* In order for the application to keep running while developing, use `nodemon` by setting ` "dev": nodemon --exec electron . ` in the package.json file and then run `npm run dev` in the terminal.

* In order to set node environment and use it in your code to check if you are in devoloping mode or not, insert `"app": "set NODE_ENV=dev&& electron ."` in the `package.json` file.

* If a module downloaded from npm does not run in your electron app and your app craches, it's because this module is compiled for a different version of V8 engine which is installed by node. Electron comes with its own version of node runtime which might not be the same as the node runtime that is installed on the system. In order to solve this problem we need to first install `npm install --save-dev electron-rebuild` which is a command line tool and then run `electron-rebuild nameofmodule` in the command line. An awesome approach would be to add `"postinstall": "electron-rebuild"` in the package.json file so that after each `install` of a module, a `postinstall` will automatically run.

* In order to debug node apps using chrome dev tools, run `node --inspect-brk=9229 index.js` in terminal. Then on a new chrome tab move to `chrome://inspect/`. You can chage the port from 9229 to any other number greater than 1023.

* using `once` for listening to an event will discard the listener after the event is triggered for the first time.

* To make a child window appear on the top of the main window for some seconds and then disappears, call `settimeout()` twice.

* In the style.css of the windows, set `user-select:none` for the `body` element in order to prevent user being able to select text on the app window.

* In order to make a frameless window draggable, set `webkit-app-region:drag` as an inline style.

* Install `electron-window-state` to save and restore your app windows sizes. 


