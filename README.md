# yolo-log-parser

A program for parsing yolo logs

## Usage

```
var LogParse = require('yolo-log-parser')
var parser = new LogParse()

fs.createReadStream('yolo.log').pipe(parser)

parser.on('data', function (c) {
  // this is the raw data, don't know why you need this, but whatever
})

parser.on('message', function (message) {
  // this is probably what you want.
  // it's the parsed object with informative fields
})
```

## Fields

The parsed messages all have these fields:

* `date` The date that the log was posted
* `level` Usually one of info, log, or error
* `type` Either 'http', 'controller', 'model'  or 'misc'

Depending on the `type` they may have the following fields as well:

### http

* `ip` The requesting IP.  (If you're behind a proxy or load balancer,
  then it's not super interesting.)
* `method` Something like GET, POST, PUT, etc.
* `url` The url requested
* `statusCode` The response status code.
* `userAgent`
* `responseTime`

### controller

* `controller` 
* `method` 

### model

* `model` 
* `action`
* `id`

### misc

* `message` Whatever it was that couldn't be parsed.
