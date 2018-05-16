---
title: Using Time zones
---

There are two interfaces for using time zones with Moment.js.

`moment.tz(..., String)` is used to create a moment in some time zone

```js
var format = "MMMM Do YYYY, HH:mm:ss Z zz";
  
var a = moment.tz("2013-11-18 11:55", "Asia/Taipei");
var b = moment.tz("2013-11-18 11:55", "America/Toronto");
  
a.format(format); // November 18th 2013, 11:55:00 +08:00 CST
b.format(format); // November 18th 2013, 11:55:00 -05:00 EST
  
a.format(); // 2013-11-18T11:55:00+08:00
b.format(); // 2013-11-18T11:55:00-05:00

```
Please note that in this case `a` and `b` are not equal moments in time, there's a 13-hour difference between `11:55` in Taipei and `11:55` in Toronto:

```js   
a.valueOf() === b.valueOf(); // false  
a.diff(b, 'hours'); // -13
```

  
  
`moment().tz(String)` is used to set a time zone in which existing moment should be represented:

```js 
var c = moment("2013-11-18 11:55");  
  
c.tz("Asia/Taipei").format(format);  // November 18th 2013, 18:55:00 +08:00 CST
c.tz("Asia/Toronto").format(format); // November 18th 2013, 05:55:00 -05:00 EST
```

So, when you call `.tz()` this way, you first get `2013-11-18 11:55` in your default timezone (`Europe/Rome` for example) and then tell Moment to format that moment for another timezone.