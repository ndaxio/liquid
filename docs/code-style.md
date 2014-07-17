# Coding Style

Notes regarding coding style in this package.

Node.js has several conflicting Best Practices, so we're going to pick one and
stick with it.


* Indent: 4 spaces.

* Semicolons: Always.

* Naming: camelCase by default. TitleCase for classes.

* Reusable code in ./lib

* Module definitions:
  ```
  var Foo = module.exports.Foo = function() {
    ...
  };
  ```

* Require blocks:
  ```
  var foo = require('foo'),
      bar = require('bar'),
      baz = require('baz');
  ```

* Preferred tools:
  * Async: async
  * APIs: bitstamp-request, bitstamp-ws, bitme
  * Command-line flag parsing: commander?
  * Database/state: (sqlite3?) sequelize?
  * Email: ?
  * Logging: bole?
  * Testing: Mocha
  * Websockets: socket.io? (Lots of options, not clear which is best atm.)

* 'use strict';?