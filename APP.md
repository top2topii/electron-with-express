# How to run express within electron?
- https://stackoverflow.com/questions/39020525/how-to-run-express-within-electron

## Detail Information
- main.js 안에 아래의 코드를 createWindow() 안에 최상단에 추가
```javascript
// Instantiate Express App
app.server = require(__dirname + '/app/app')();
```
- /app/app.js 작성
```javascript
module.exports = () => {
  // Load The FS Module & The Config File
  fs = require('fs');

  // Load The Path Module
  path = require('path');

  config = JSON.parse(fs.readFileSync('config.json'));

  // Load Express Module
  express = require('express');
  app 	= express();

  app.get('/', function(req, res) {
    res.send("Hello world! Express Server Works!");
  });

  app.listen(config.server.port, function () {
    console.log('Express server listening on port ' + config.server.port);
  });
}

```
- /config.js 작성
```json
{
  "server": {
	"host": "localhost",
	"port": 3000
  },
  "session": {
	"secret": "MySuper Secret hhhkkk"
  }
}
```
