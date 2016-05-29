simple-cli-parser
=================

[![Build Status](https://travis-ci.org/leemm/simple-cli-parser.svg?branch=master)](https://travis-ci.org/leemm/simple-cli-parser)

A simple parser for spawning a child_process, with promises/ES6 style classes.

# Install
```
npm install simple-cli-parser --save
```

# Usage

To see the result of ls -la.

```javascript
'use strict';

const cli = require('simple-cli-parser');

let download = new cli([ 'ls', '-la', __dirname ])
    .then(res => { console.log('Success!', res); })
    .catch(err => { console.log('Failed!'); });
```

To stream the result of a curl download (to check current percentage).

```javascript
'use strict';

const cli = require('simple-cli-parser'),
    currentPercentage = data => { // Optional function for checking status
        let percent = parseFloat(data, 10);
        if (!isNaN(percent) && percent > 0){ console.log(percent + '%'); }
    };

let download = new cli([ 'curl', '-O', 'http://speedtest.ftp.otenet.gr/files/test10Mb.db', '-#' ], currentPercentage)
    .then(res => { console.log('Success!', res); })
    .catch(err => { console.log('Failed!'); });
```