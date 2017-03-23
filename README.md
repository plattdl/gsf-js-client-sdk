# GSF JavaScript Client SDK
[![Build Status](https://travis-ci.org/geospatial-services-framework/gsf-js-client-sdk.svg?branch=master)](https://travis-ci.org/geospatial-services-framework/gsf-js-client-sdk)
## About the SDK
The GSF JavaScript Client SDK provides a client-side JavaScript library for interacting with GSF.  For detailed information please visit our [full developer documentation] page.

1. This repository contains pre-built distributable files located in the `/dist/` directory.
    - `/dist/GSF.js` - The non-minified bundle.
    - `/dist/GSF.map.js` - The non-minified bundle source map file.
    - `/dist/GSF.min.js` - The minified bundle.
    - `/dist/GSF.min.js.map` - The minified bundle source map file.

## Installation
The SDK can be installed using [npm].

    $ npm install gsf-js-client-sdk

## Basic Usage
#### Module Import
1. After installing with npm, import the sdk into your file:

`import * as GSF from 'gsf-js-client-sdk`

#### Script Tag
1. Include the GSF JavaScript Client SDK file in your project.  The example below assumes the SDK file is located next to your html file.

    `<script src="GSF.min.js"></script>`

2. Access the SDK using the global GSF object.

    `<script>console.log(GSF);</script>`

#### Basic Example

1. Below is a simple example of running a job and retrieving the results.  You will need to update the server address and port below to reflect the server that you are using.

```javascript
// GSF Server
const server = GSF.server({
  address: 'MyServer',
  port: '9191'
  });

// Create a service object.
const service = server.service('ENVI');

// Create a task object.
const task = service.task('SpectralIndex');

const NDVIParameters = {
  parameters: {
    INPUT_RASTER: {
      FACTORY: 'URLRaster',
      URL: 'http://MyServer:9191/ese/data/qb_boulder_msi'
    },
    INDEX: 'Normalized Difference Vegetation Index'
  }
};

// Submit a job.
task.submitAndWait(NDVIParameters).then((results) => {
    // Do something with results.
    AddToMap(results.OUTPUT_RASTER);
  }).catch((err) => {
    // Display error.
  });
```

This is just a sample of what can be done with the SDK.  Please see our [full developer documentation] to learn more.

## Requirements
The GSF JavaScript Client SDK relies on [server-sent events] for communication with the server.  Developers who wish to build apps that run on browsers lacking EventSource support may want to use a polyfill.

## Developer Documentation
Please visit our [full developer documentation] page for more information.


[full developer documentation]: https://geospatial-services-framework.github.io/sdk-docs/
[npm]:http://npmjs.com
[server-sent events]:https://www.w3schools.com/html/html5_serversentevents.asp
