# electron-video
## First taste of electron

* `ffmpeg` is the most popular command line tool to work with video files. `fluent-ffmpeg` is the wrapper which makes it easier to work with `ffmpeg`.

* `app` object is responsible for runnig electron process on our machine.

* whenever we need to make a menu, first we need to make a menu template. It's an object or an array which is the structure of the menu.

* If you need to check what platform your app is running on, run `process.platform` on your index.js. If it's MacOS it will be equal to `darwin`. If it's windows, it's `win32`.

* when inside an object, you can use `IIFE` to decide what value to assign to a property of the object. In electron you need to use an IIFE for the `accelerator` property of a `submenu` object.

* If you need to check whether you are in development or production mode, check `process.env.NODE_ENV`. Possible values are `production, staging, development`

* In electron, whenever we close a window, we have to assign the window object to `null` so that the JS garbage collector would know that it can reclaim the memory which was occupied by the window. 
