# node-modules-path [![Build Status](https://travis-ci.org/ember-cli/node-modules-path.svg)](https://travis-ci.org/ember-cli/node-modules-path)

Determine the `node_modules` path for a given project even when outside a project's root.

A utility function for determining what path an addon may be found at. Addons
will only be resolved in the project's own `node_modules/` directory, they
do not follow the standard node `require` logic that a standard
`require('mode-module')` lookup would use, which finds the module according
to the `NODE_PATH`.

## Why?

Possible use cases for this include caching
the `node_modules/` directory outside of a source code checkout, and
ensuring the same source code (shared over a network) can be used with
different environments (Linux, OSX) where binary compatibility may not
exist.

For example, if you have a project in `/projects/my-app` and its `node_modules`
directory is at `/resource/node_modules`, you would:

```
  # Node uses this as its search path for standard `require('module')` calls
  export NODE_PATH=/resource/node_modules

  # So that ember addon discovery looks here
  export EMBER_NODE_PATH=/resource/node_modules

  cd /projects/my-app && ember build
```

## Installation

```sh
npm install --save node-modules-path
```

## Usage

```js
var nodeModulesPath = require('node-modules-path');

nodeModulesPath(cwd());  // => '/Users/tomster/some-project/node_modules'
```
