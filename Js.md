**Get the option value which selected from user**
```
<select id="userOption">
  <option value="1">test1</option>
  <option value="2" selected="selected">test2</option>
  <option value="3">test3</option>
</select>
```

Running this code  
```
var e = document.getElementById("userOption");
var userSelection = e.options[e.selectedIndex].value;
```
Would make userSelection be 2.  

If what you actually want is test2, then do this:
```
var e = document.getElementById("userOption");
var userSelection = e.options[e.selectedIndex].text;
```
Which would make userSelection be test2
