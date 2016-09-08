Tribune's Bootstrap 3 JavaScript for Browserify
===============================================

The Chicago Tribune's DataViz team uses a [custom build of Bootstrap 3](https://github.com/newsapps/bootstrap/) as the starting point for projects that live outside of the company's CMS.  We've started to bundle our Javascript using Browserify. Not only does this reduce the number of requests when loading a page, it makes static sites JavaScript available, even if a CDN goes away.

To use in your project, first install using npm:

    npm install --save git+https://github.com/newsapps/tribune-bootstrap-3-js.git

Then in your project:

    var $ = require('jquery');
    require('tribune-bootstrap-3-js');

    // Do stuff with the Bootstrap jQuery plugins ...

We've also started using [npm scripts](https://docs.npmjs.com/misc/scripts) to build front-end assets.  Including Bootstrap in a vendor bundle might have a `package.json` that looks something like this:

    "config": {
    "requireargs": "--require jquery --require tribune-bootstrap-3-js",
    "externalargs": "--external jquery --external tribune-bootstrap-3-js"
    },
    "scripts": {
      "test": "echo \"Error: no test specified\" && exit 1",
      "build:scripts:vendor": "browserify $npm_package_config_requireargs --debug --plugin [minifyify --map vendor.min.js.map --output js/vendor.min.js.map]  > js/vendor.min.js",
      "build:scripts:app": "browserify $npm_package_config_externalargs --debug --plugin [minifyify --map app.min.js.map --output js/app.min.js.map] > js/app.min.js"
    }

