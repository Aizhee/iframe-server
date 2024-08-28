[![view on npm](http://img.shields.io/npm/v/iframe-server.svg)](https://www.npmjs.org/package/iframe-server)

IFrame-Server
===========

A modified and lite version of [Live-Server](https://github.com/tapio/live-server) by Tapio to allow javascript injection for iframe content with CORS protection such as vscode webview. 

Installation
------------

You need node.js and npm. You should probably install this globally.

**Npm way**

	npm install -g iframe-server

**Manual way**

	git clone https://github.com/Aizhee/iframe-server
	cd iframe-server
	npm install 

Usage from command line
-----------------------

Issue the command `iframe-server` in your project's directory. Alternatively you can add the path to serve as a command line parameter.

This will automatically launch the default browser. When you make a change to any file, the browser will reload the page - unless it was a CSS file in which case the changes are applied without a reload.

Command line parameters:

* `--port=NUMBER` - select port to use, default: PORT env var or 8080
* `--host=ADDRESS` - select host address to bind to, default: IP env var or 0.0.0.0 ("any address")
* `--no-browser` - suppress automatic web browser launching
* `--browser=BROWSER` - specify browser to use instead of system default
* `--quiet | -q` - suppress logging
* `--verbose | -V` - more logging (logs all requests, shows all listening IPv4 interfaces, etc.)
* `--open=PATH` - launch browser to PATH instead of server root
* `--watch=PATH` - comma-separated string of paths to exclusively watch for changes (default: watch everything)
* `--ignore=PATH` - comma-separated string of paths to ignore ([anymatch](https://github.com/es128/anymatch)-compatible definition)
* `--no-css-inject` - reload page on CSS change, rather than injecting changed CSS
* `--entry-file=PATH` - serve this file (server root relative) in place of missing files (useful for single page apps)
* `--mount=ROUTE:PATH` - serve the paths contents under the defined route (multiple definitions possible)
* `--wait=MILLISECONDS` - (default 100ms) wait for all changes, before reloading
* `--htpasswd=PATH` - Enables http-auth expecting htpasswd file located at PATH
* `--cors` - Enables CORS for any origin (reflects request origin, requests with credentials are supported)
* `--https=PATH` - PATH to a HTTPS configuration module
* `--https-module=MODULE_NAME` - Custom HTTPS module (e.g. `spdy`)
* `--help | -h` - display terse usage hint and exit
* `--version | -v` - display version and exit
* `--script` - add your own custom javascript code to be injected

Default options:

If a file `~/.iframe-server.json` exists it will be loaded and used as default options for iframe-server on the command line. See "Usage from node" for option names.


Usage from node
---------------

```javascript
var iframeServer = require("iframe-server");

var params = {
	port: 8181, // Set the server port. Defaults to 8080.
	host: "0.0.0.0", // Set the address to bind to. Defaults to 0.0.0.0 or process.env.IP.
	root: "/public", // Set root directory that's being served. Defaults to cwd.
	open: false, // When false, it won't load your browser by default.
	ignore: 'scss,my/templates', // comma-separated string for paths to ignore
	file: "index.html", // When set, serve this file (server root relative) for every 404 (useful for single-page applications)
	wait: 1000, // Waits for all changes, before reloading. Defaults to 0 sec.
	mount: [['/components', './node_modules']], // Mount a directory to a route.
	logLevel: 2, // 0 = errors only, 1 = some, 2 = lots
	script: `console.log("hello world!");` // javascript code to be injected in the page/iframed content
};
iframeServer.start(params);
```


License
-------

Uses MIT licensed code from [Connect](https://github.com/senchalabs/connect/), [Roots](https://github.com/jenius/roots), and[Live-Server](https://github.com/tapio/live-server).

(MIT License)

Copyright (c) 2024 Aizhee

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
