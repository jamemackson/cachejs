# CacheJS

forked from code.google.com/p/cachejs

Cachejs allows you to cache, with expiries, all kinds of data.

It depends upon no external libraries. 

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



You don’t need to worry about serialising values; the cache internally json encodes the value if needed when setting, and parses it again before returning it back to you, keeping the interface nice and clean, and allowing you to store any kind of data – raw JSON, XML, variables, objects, strings, etc.

What’s more, it’s designed to be future-proof, with pluggable storage modules allowing you to extend the caching object to use any kind of storage system. The cache API abstracts the storage API away so you can swap stores without changing your caching code at all; you just change the setStore line and the rest of the code will still work just fine.

We’ve written an arrayStore which caches data for the current page only, a cookieStore which works for the whole domain but has the usual cookie limits, and a localstorageStore which uses the funky HTML5 Web Storage specification (AFAIK supported by IE8, FF3.5, Safari4, Chrome4, Opera10).