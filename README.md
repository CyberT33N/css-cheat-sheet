# CSS Cheat Sheet
CSS Cheat Sheet with the most needed stuff..
<br />
<br />
<br />
<br />


# Golden Rules

- Use RGBA for fill
```css
/*correct*/
fill:(rgba(181, 188, 255, 0.6))
/*may bugs with some color codes and fill cant read the color value and will choose black instead!*/
fill:(#09bde0b3)
```

<br />
<br />


 _____________________________________________________
 _____________________________________________________


<br />
<br />


# Center Vertical
```css
/* Method #1 */
margin: 0;
position: absolute;
top: 50%;
-ms-transform: translateY(-50%);
transform: translateY(-50%);

/* Method #2 */
.outer {
  position: absolute;
  display: table;
  width: 100%;
  height: 100%;
  text-align: center;
}
.middle {
  display: table-cell;
  vertical-align: middle;
}

/* Method #3 */
.parent {
    width: 400px;
    height:200px;
    display: flex;
}

.child {
    width: 75px;
    height: 75px;
    margin-top:auto;
    margin-bottom:auto;
}

```  



# Center Horizontal
```css
/* Method #1 */
display: block;
margin-left: auto;
margin-right: auto;
```  



# Center Horizontal & Vertical
```css

/* Method #1 */
position: fixed;
top: 50%;
left: 50%;
transform: translate(-50%, -50%);

/* Method #2 */
.parent {
    width: 400px;
    height:200px;
    display: flex;
}

.child {
    width: 75px;
    height: 75px;
    margin:auto;
}

```  


<br />
<br />


 _____________________________________________________
 _____________________________________________________


<br />
<br />


# Auto height/width to parent
```css
/* Method #1 */
height: inherit;
```  

# Auto height & width to parent (flex-grow)
```css
/* Method #1 */
#main {
   display: flex;
   width:100%;
}
#child{
    flex-grow: 1;
}
```  


# Auto scale SVG to parent
```css
/* Method #1 (change inside of svg) */
 width="100%"
 height="100%"
 viewBox="113 128 972 600"
 preserveAspectRatio="xMidYMid meet"
```  


<br />
<br />


 _____________________________________________________
 _____________________________________________________



<br />
<br />


# Align two DIV next to each other
```css
/* Method #1 */
#wrapper {
    width: 500px;
    border: 1px solid black;
    overflow: hidden; /* will contain if #first is longer than #second */
}
#first {
    width: 300px;
    float:left; /* add this */
    border: 1px solid red;
}
#second {
    border: 1px solid green;
    overflow: hidden; /* if you don't want #second to wrap below #first */
}
```  


# Align two DIV next to each other and let right one fit the parent wrapper
```css
/* Method #1 */
.wrapper{
    width: 90%;
    height: 2.5em;
    display: flex;
}
.child-left {
    position: relative;
    display: flex;
    width: 160px;
}
.child-right {
    flex-grow: 1;
    flex-direction: column;
    position: relative;
    height: 35px;
}
```  



# Align multiple DIV under each other (label tag)
```html
/* Method #1 */
<div class="editor-label-wrapper">
  <label class="editor-label-one">Anything inside here as example more divs..</label>
  <label class="editor-label-two">Anything inside here as example more divs..</label>
  <label class="editor-label-three">Anything inside here as example more divs..</label>
</div>
```  





<br />
<br />


 _____________________________________________________
 _____________________________________________________


<br />
<br />



# Box Shadow Top & Bottom only
```css
/* Method #1 */
  box-shadow: 
        inset 0px 11px 8px -10px #CCC,
        inset 0px -11px 8px -10px #CCC; 
```  



<br />
<br />


 _____________________________________________________
 _____________________________________________________


<br />
<br />



# Z-index not working
```css
/* Method #1 (disable pointer events of the layer which is blocking the element which needs to be clicked) */
    pointer-events: none;
```  



<br />
<br />


 _____________________________________________________
 _____________________________________________________


<br />
<br />


# Scrollbar Definition
![alt tag](https://i.stack.imgur.com/V1ElK.png)



<br />
<br />

 _____________________________________________________
 _____________________________________________________


<br />
<br />


# Disable scroll for user
```css
:root {
  scroll-behavior: smooth;
}

html.noscroll{
    position: fixed;
    width: 100%;
    top:0;
    left: 0;
    height: 100%;
    overflow-y: scroll !important;
    z-index: 10;
 }
```


```javascript

          let el = $("layertwo");
          let position = el.position();
         console.log( "left: " + position.left + ", top: " + position.top );

        setTimeout(() => { $('html').toggleClass('noscroll').css('top', '-' + position.top + 'px');  },500);

        setTimeout(() => {
          $('html').removeClass('noscroll');

        let root = document.querySelector(':root');
        root.setAttribute("style", "scroll-behavior: auto;");

          window.scrollTo({
              top: $('layertwo').offset().top,
              left: 0
            });

        root.setAttribute("style", "scroll-behavior: smooth;");

      },5000);

```


<br />
<br />

 _____________________________________________________
 _____________________________________________________


<br />
<br />

# Other

## Reset gradient animation
```javascript
var elbg = document.querySelector('headerBIG');
elbg.style.animation = 'none';
elbg.offsetHeight; /* trigger reflow */
elbg.style.animation = null;
```

<br />
<br />

 _____________________________________________________
 _____________________________________________________


<br />
<br />




# Nice Colors Collection

## white
```css
color: #f7f7f7;
color: #f1f1f1;
color: #e1e1e1;
color: #f8f8f8;
```

## box-shadow inset
```css
box-shadow: inset 0 0 0.7vmax -0.3vmax #000000d1;
```


<br />
<br />

 _____________________________________________________
 _____________________________________________________


<br />
<br />

# Nice Fonts Collection

## Signature
```css
@import url('https://fonts.googleapis.com/css?family=Bilbo+Swash+Caps&display=swap');
@import url('https://fonts.googleapis.com/css?family=Alex+Brush&display=swap');
```

## General Text
```css
@import url('https://fonts.googleapis.com/css?family=Roboto&display=swap');
```


<br />
<br />

 _____________________________________________________
 _____________________________________________________


<br />
<br />



# Third Party Collections

## Loading screens
- https://tobiasahlin.com/spinkit/

## Close Button
- Animated Close Buttons: https://codepen.io/JonasBadalic/pen/MYaMBz

## Hover
- Button hover effects with box-shadow: https://codepen.io/giana/pen/BZaGyP

## Converter
- Google Fonts Offline Downloader: https://google-webfonts-helper.herokuapp.com
- Image Compressor: https://imagecompressor.com

## Anime.js
- Animated Letters: https://tobiasahlin.com/moving-letters/
- Staggering: https://codepen.io/juliangarnier/pen/XvjWvx
- Login Box: https://codepen.io/ainalem/pen/EQXjOR
- Submit Button: https://codepen.io/andrewmillen/pen/MoKLob
- Animated Hand Signature: https://codepen.io/mellis84/pen/JpVZNw


#### Background
- Animated Background: https://codepen.io/juliangarnier/pen/ZeEpgd
- Background Color Change: https://codepen.io/alexzaworski/pen/mEkvAG

