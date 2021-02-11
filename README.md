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
 
