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