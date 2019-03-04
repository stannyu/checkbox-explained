## **Custom checkboxes** ##


### **1. Simple approach** ###

Basic markup:
```javascript 
<label class="check option">
  <input class="check__input" type="checkbox">
  <span class="check__box"></span>
  First
</label>
```

Default checkbox hidden by: 
```css 
.check__input {
    position: absolute;
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
}
```
```position: absolute``` used for removing space in front of label text.

#### Main principles ####
- No need to use atribute 'for' when input nested in label.<br>
- Main issue is not to hide default browser checkbox with 'display: none;'.<br>
- In this simple case I used 'appearance: none' with vendor prefixes.
<br>

Background images are external for all of the assets.
Checkboxes stylings handled with combination of default checkbox state folowed by custom checkbox class.

```css
/* Checked */
 .check__input:checked + .check__box {
   background: url(images/on.svg);
 }
/* Focused */
 .check__input:focus + .check__box {
   background: url(images/off-focused.svg);
 } 
/* Focused and Checked */
 .check__input:checked:focus + .check__box {
   background: url(images/on-focused.svg);
 }
/* Disabled */
 .check__input:disabled + .check__box {
   background: url(images/off-disabled.svg);
 }
/* Disabled and Checked */
 .check__input:checked:disabled + .check__box {
   background: url(images/on-disabled.svg);
 }
```


The reason that I didn't completely hide checkbox, except accessibility, is that
styles now could be anchored to this checkbox and used to control states of checkbox.
<br>

There is also an issue with this method.
The issue is that every checkbox state image is external.
That means that if user have slow connection and checked checkbox - checked state image can be lost
or stack somewhere in between client and server.
<br> 

### **2. Inlined images approach** ###
To inline SVG into CSS I used [this awesome website](https://yoksel.github.io/url-encoder/ru/).
<br>

So instead
```css
.check__input:checked:disabled + .check__box {
    background: url(images/on-disabled.svg);
}
```
We have now
```css
.check__input:checked:disabled + .check__box {
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://   www.w3.org/2000/svg' viewBox='0 0 20 20'%3E%3Crect x='2' y='2' width='16' height='16' fill='%239B9B9B' rx='3'/%3E%3Cpolyline fill='none' stroke='%23FFF' stroke-width='3' points='5 9 9 13 15 6'/%3E%3C/svg%3E");
}
```

CSS styled checkboxes will work when you have relatively simple graphics only. Otherwise it will be an overhead.

### **3. Styled with CSS** ###

As graphics is simple in this case we can handle checkboxes stylings with css.

```.check__box``` styles changed just to style element the same way as our SVG graphics.

The mosty important point is that now we can style elements by background color and check.svg icon:

```css
.check__input:checked + .check__box {
    background-color: #4A90E2;
    background-image: url(images/check.svg);
  }
```

To handle 'Focus' state we can apply box-shadow property with two shadows:

```css
.check__input:focus + .check__box {
  box-shadow:
    0 0 0 0.1em #4A90E2,
    0 0 0 0.2em #7ED321;
}
```
In this case we do not need to style focused and checked state as we combining states with styles. 

So this definition 
``` .check__input:checked:focus + .check__box``` is not necessary any more!

Disabled and Checked - Disabled share the same idea.
```css
/* Disabled */
.check__input:disabled + .check__box {
  box-shadow: 0 0 0 0.1em #9B9B9B;
}
/* Disabled and Checked */
.check__input:checked:disabled + .check__box {
  background-color: #9B9B9B;
}
```