### **Custom checkboxes** ###

```javascript 
<label class="check option">
  <input class="check__input" type="checkbox">
  <span class="check__box"></span>
  First
</label>
```

#### Main principles ####
- No need to use atribute 'for' when input nested in label.<br>
- Main issue is not to hide default browser checkbox with 'display: none;'.<br>
- In this simple case I used 'appearance: none' with vendor prefixes.

<br>
The reason that I didnt completely hide checkbox, except accessibility, is that
  styles now could be anchored to this checkbox and used to control states of checkbox.
<br>

There is also an issue with this method.
The issue is that every checkbox state image is external.
That means that if user have slow connection and checked checkbox - checked state image can be lost
or stack somewhere in between client and server.

<br> 
To inline SVG into CSS I used [this awesome website](https://yoksel.github.io/url-encoder/ru/).
<br>

CSS styled checkboxes will work when you have relatively simple graphics only. Otherwise it will be an overhead.