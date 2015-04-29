# CacheJS

forked from code.google.com/p/cachejs

## example usage

```html
<html>
<head>
  <title></title>
  <script type="text/javascript" src="json.js"></script>
  <script type="text/javascript" src="cache.js"></script>
  <script type="text/javascript" src="stores.js"></script>
  <script type="text/javascript">
  function load() {
    var myCache = cache();
    // setting a value which does not expire:
    alert("Is non-existant value set (should be FALSE): "+myCache.has('foo')); // false
    myCache.set('foo',"val");
    alert("Is existing value set (should be TRUE): "+myCache.has('foo')); // true
    alert("Value (should be \"val\"): "+myCache.get('foo')); // "val
    // setting a value which does expire:
    var tomorrow = new Date();
    tomorrow.setTime(tomorrow.getTime() + (1000*3600*24));
    myCache.set('foo',"val",tomorrow);
    alert("This value expires tomorrow: "+myCache.get('foo')); // "val", until tomorrow, at which point it will return undefined
    var yesterday = new Date();
    yesterday.setTime(yesterday.getTime() - (1000*3600*24));
    myCache.setExpiry('foo',yesterday);
    alert("Now it has expired and should be NULL: "+myCache.get('foo')); // null
  }
  </script>
</head>
<body onload="load();">
</body>
</html>
```