# CSS Cheat Sheet
CSS Cheat Sheet with the most needed stuff..
<br />
<br />
<br />
<br />


# Modify text

## Force Line Break after space
```css
/* Method #1 */
word-spacing: 100vw;
}
```  



<br />
<br />


 _____________________________________________________
 _____________________________________________________


<br />
<br />

# Responsive Tutorials
- https://1linelayouts.glitch.me/



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

/* Method #2 */
position: fixed;
left: 50%;
transform: translate(-50%, 0%);
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


# Auto height & width image to div without stretch
```css
/* Method #1 */
  background-image: url("http://i.stack.imgur.com/2OrtT.jpg");
  background-size: cover;
  background-repeat: no-repeat;
  background-position: 50% 50%;
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
/* Method #1 use display:block on the labels if needed*/
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



# Box Shadow Top & Bottom
```css
/* Method #1 */
  box-shadow: 
        inset 0px 11px 8px -10px #CCC,
        inset 0px -11px 8px -10px #CCC; 
```  

# Box Shadow Bottom
```css
/* Method #1 */
box-shadow: 0 8px 6px -6px #00000052;
```  

# Box Shadow Left & Right
```css
/* Method #1 */
box-shadow: 0 9px 0px 0px #ffffff00,
0 -9px 0px 0px #ffffff00,
0px 10px 15px -6px #00000042,
0px 10px 15px -6px #00000042;
```  

    

<br />
<br />


 _____________________________________________________
 _____________________________________________________


<br />
<br />

# Transition

## Add delay to specific property
```css
transition: height 0.35s ease, 
            width 0.35s ease, 
            margin 0.35s ease, 
            border-color 0.35s 0.35s ease; /* notice how the delay is added here alone */
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


# Disable scroll for user

## Method 1
```css
$( 'body' ).css( 'overflow', 'hidden' );
```

## Method 2
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

## Reset animation
```javascript
$( '.circles li' ).css( 'animation', 'none' );
await new Promise(resolve => setTimeout(resolve, 100));
$( '.circles li' ).css( 'animation', '' ); // it will catch the default settings in your css
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

## light grey
```css
color: #d8d8d8;
color: #dfdfdf;
color: #d5d5d5;
```

## light red
```css
color: #f15044;
```

## black
```css
color: #333333;
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
//font-family: 'Baloo Chettan 2', cursive;
@import url(https://fonts.googleapis.com/css2?family=Baloo+Chettan+2&display=swap);

font-family: Raleway, sans-serif;

@import url(https://fonts.googleapis.com/css?family=Work+Sans);
@import url(https://fonts.googleapis.com/css?family=Work+Sans:400,500,600,700);
font-family: "Open Sans", sans-serif;
```


    

## Headline 
```css
/*https://fonts.google.com/specimen/Alfa+Slab+One?sort=popularity*/
@import url('https://fonts.googleapis.com/css2?family=Alfa+Slab+One&display=swap');

/*https://fonts.google.com/specimen/Audiowide?sort=popularity&preview.text=Latest+Projects&preview.text_type=custom
font-family: 'Audiowide', cursive;
*/
@import url('https://fonts.googleapis.com/css2?family=Audiowide&display=swap');

/*https://fonts.google.com/specimen/Days+One?sort=popularity&preview.text=Latest+Projects&preview.text_type=custom&sidebar.open&selection.family=Days+One
font-family: 'Days One', sans-serif;
*/
@import url('https://fonts.googleapis.com/css2?family=Days+One&display=swap');
```

<br />
<br />

 _____________________________________________________
 _____________________________________________________


<br />
<br />

# Chrome Inspector Custom Devices 
As example on windows you can find this file:
- AppData\Local\Chromium\User Data\Your profile here or default\Preferences

Inside of this json file you search for this path:
- devtools.preferences.customEmulatedDeviceList

Then you can add this here for custom devices:
```javascript
"customEmulatedDeviceList":"[{\"title\":\"Desktop - FHD - 1920x1080\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1920,\"height\":1080},\"horizontal\":{\"width\":1080,\"height\":1920}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Always\"},{\"title\":\"Desktop 2700x900\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":2700,\"height\":900},\"horizontal\":{\"width\":900,\"height\":2700}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"desktop -  4k - 3840x2160\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":3840,\"height\":2160},\"horizontal\":{\"width\":2160,\"height\":3840}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Always\"},{\"title\":\"desktop - 4k other - 3440x1440\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":3440,\"height\":1440},\"horizontal\":{\"width\":1440,\"height\":3440}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Always\"},{\"title\":\"desktop - QHD - 2560x1440\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":2560,\"height\":1440},\"horizontal\":{\"width\":1440,\"height\":2560}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Always\"},{\"title\":\"desktop - 4k other v2 - 2560x1080\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":2560,\"height\":1080},\"horizontal\":{\"width\":1080,\"height\":2560}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"desktop - WUXGA - 1920x1200\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1920,\"height\":1200},\"horizontal\":{\"width\":1200,\"height\":1920}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"desktop -   WSXGA+   - 1680x1050\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1680,\"height\":1050},\"horizontal\":{\"width\":1050,\"height\":1680}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"desktop -   HD+   - 1600x900\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1600,\"height\":900},\"horizontal\":{\"width\":900,\"height\":1600}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Always\"},{\"title\":\"desktop - hd other v1 - 1536x864\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1536,\"height\":864},\"horizontal\":{\"width\":864,\"height\":1536}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Always\"},{\"title\":\"desktop -    WXGA+   - 1440x900\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1449,\"height\":900},\"horizontal\":{\"width\":900,\"height\":1449}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"desktop - hd default v1 - 1366x768\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1366,\"height\":768},\"horizontal\":{\"width\":768,\"height\":1366}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"desktop - hd default v2 smaller - 1360x768\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1360,\"height\":768},\"horizontal\":{\"width\":768,\"height\":1360}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"desktop - SXGA - 1280x1024\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1280,\"height\":1024},\"horizontal\":{\"width\":1024,\"height\":1280}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"desktop - WXGA v3 - 1280x800\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1280,\"height\":800},\"horizontal\":{\"width\":800,\"height\":1280}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"desktop - WXGA v2 - 1280x768\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1280,\"height\":768},\"horizontal\":{\"width\":768,\"height\":1280}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"desktop - WXGA v1 - 1280x720\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1280,\"height\":720},\"horizontal\":{\"width\":720,\"height\":1280}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Always\"},{\"title\":\"desktop -    XGA+    - 1152x864\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1152,\"height\":864},\"horizontal\":{\"width\":864,\"height\":1152}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"desktop - XGA - 1024x768\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1024,\"height\":768},\"horizontal\":{\"width\":768,\"height\":1024}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"desktop - WSVGA - 1024x600\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1024,\"height\":600},\"horizontal\":{\"width\":600,\"height\":1024}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Always\"},{\"title\":\"desktop - SVGA - 800x600\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":800,\"height\":600},\"horizontal\":{\"width\":600,\"height\":800}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"tablet - ipad/ipad mini - 768x1024\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (iPad; CPU OS 6_0 like Mac OS X) AppleWebKit/536.26 (KHTML, like Gecko) Version/6.0 Mobile/10A406 Safari/8536.25\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":768,\"height\":1024},\"horizontal\":{\"width\":1024,\"height\":768}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Always\"},{\"title\":\"tablet - ipad pro - 1024x1366\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (iPad; CPU OS 11_3 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/11.0 Mobile/15E148 Safari/604.1\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1024,\"height\":1366},\"horizontal\":{\"width\":1366,\"height\":1024}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"tablet - nexus 7(2013) - 600x960\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (Linux; Android 4.4; Nexus 7 Build/KRT16M) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/30.0.1599.92 Safari/537.36\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":600,\"height\":960},\"horizontal\":{\"width\":960,\"height\":600}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"tablet-GalaxyTab 10/kindle hdx/nexus10 - 800x1280\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (Linux; Android 4.4.2; Nexus 10) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.110 Safari/537.36\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":800,\"height\":1280},\"horizontal\":{\"width\":1280,\"height\":800}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"tablet - Chromebook Pixel - 1280x850\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (Linux; Android 9; Mediatek MT8173 Chromebook Build/R80-12739.94.0; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/80.0.3987.132 Safari/537.36MoodleMobile escoffier\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1280,\"height\":850},\"horizontal\":{\"width\":850,\"height\":1280}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"handy - iPhone XS Max/XR - 414 x 896\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (iPhone; CPU iPhone OS 13_3_1 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Mobile/15E148 [FBAN/FBIOS;FBDV/iPhone11,6;FBMD/iPhone;FBSN/iOS;FBSV/13.3.1;FBSS/3;FBID/phone;FBLC/en_US;FBOP/5;FBCR/]\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":414,\"height\":896},\"horizontal\":{\"width\":896,\"height\":414}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"handy - iPhone X/XS - 375 x 812\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (iPhone; CPU iPhone OS 13_3_1 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Mobile/15E148 [FBAN/FBIOS;FBDV/iPhone11,2;FBMD/iPhone;FBSN/iOS;FBSV/13.3.1;FBSS/3;FBID/phone;FBLC/en_US;FBOP/5;FBCR/]\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":375,\"height\":812},\"horizontal\":{\"width\":812,\"height\":375}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Always\"},{\"title\":\"handy - iPhone 6/7/8 - 375 x 667\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (iPhone; CPU iPhone OS 12_4_5 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Mobile/15E148 [FBAN/FBIOS;FBDV/iPhone7,2;FBMD/iPhone;FBSN/iOS;FBSV/12.4.5;FBSS/2;FBID/phone;FBLC/en_US;FBOP/5;FBCR/]\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":375,\"height\":667},\"horizontal\":{\"width\":667,\"height\":375}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"handy - iPhone 6/7/8 Plus - 414 x 736\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (iPhone; CPU iPhone OS 12_4_5 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Mobile/15E148 [FBAN/FBIOS;FBDV/iPhone7,1;FBMD/iPhone;FBSN/iOS;FBSV/12.4.5;FBSS/3;FBID/phone;FBLC/en_US;FBOP/5;FBCR/]\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":414,\"height\":736},\"horizontal\":{\"width\":736,\"height\":414}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"handy - iPhone 5 - 320 x 568\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (iPhone; CPU iPhone OS 5_0 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9A334 Safari/7534.48.3\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":320,\"height\":568},\"horizontal\":{\"width\":568,\"height\":320}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Always\"},{\"title\":\"handy - Nexus 6+6P+5X/ pixel 2 - 412 x 732\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (Linux; Android 7.0; Nexus 6 Build/NBD92G) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.83 Mobile Safari/537.36\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":412,\"height\":732},\"horizontal\":{\"width\":732,\"height\":412}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"handy - Google Pixel 3 XL - 412 x 847\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (Linux; Android 10; Pixel 3 XL) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.93 Mobile Safari/537.36\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":412,\"height\":847},\"horizontal\":{\"width\":847,\"height\":412}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"handy - Google Pixel 2 XL - 412 x 824\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (Linux; Android 10; Pixel 2 XL) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.93 Mobile Safari/537.36\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":412,\"height\":824},\"horizontal\":{\"width\":824,\"height\":412}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"handy - Samsung Galaxy Note 5/nokia 9 - 480 x 853\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (Linux; Android 6.0.1; RedMi Note 5 Build/RB3N5C; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/68.0.3440.91 Mobile Safari/537.36\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":480,\"height\":853},\"horizontal\":{\"width\":853,\"height\":480}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"handy - Samsung Galaxy S9 & Note 9 - 360 x 740\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (Linux; Android 10; Redmi Note 9S) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.106 Mobile Safari/537.36\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":360,\"height\":740},\"horizontal\":{\"width\":740,\"height\":360}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"handy-bbz30/lumia550+950/note 2+3/S3+5+7/nexus5\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (Linux; U; Android 5.0.2; en-us; Redmi Note 2 Build/LRX22G) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/42.0.0.0 Mobile Safari/537.36 XiaoMi/MiuiBrowser/2.1.1\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":360,\"height\":640},\"horizontal\":{\"width\":640,\"height\":360}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"desktop - 8K LCD TV - 7680×4320\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":7680,\"height\":4320},\"horizontal\":{\"width\":4320,\"height\":7680}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"desktop - 8k v2 - 7680-2160\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":7680,\"height\":2160},\"horizontal\":{\"width\":2160,\"height\":7680}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"handy - iPhone 4 - 320x480\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (iPhone; CPU iPhone OS 7_1_2 like Mac OS X) AppleWebKit/537.51.2 (KHTML, like Gecko) Mobile/11D257 [FBAN/FBIOS;FBAV/62.0.0.43.141;FBBV/36454510;FBRV/0;FBDV/iPhone3,2;FBMD/iPhone;FBSN/iPhone OS;FBSV/7.1.2;FBSS/2;FBCR/Orange;FBID/phone;FBLC/pl_PL;FBOP/5]\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":320,\"height\":480},\"horizontal\":{\"width\":480,\"height\":320}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"deskop - laptop touch - 1280x950\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1280,\"height\":950},\"horizontal\":{\"width\":950,\"height\":1280}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"tablet - blackberry playbook - 600x1024\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (PlayBook; U; RIM Tablet OS 1.0.0; en-US) AppleWebKit/534.8+ (KHTML, like Gecko) Version/0.0.1 Safari/534.8+\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":600,\"height\":1024},\"horizontal\":{\"width\":1024,\"height\":600}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"handy - lg optimus l70/nexus 4 - 384-640\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (Linux; Android 4.4.2; Nexus 4 Build/KOT49H) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/34.0.1847.114 Mobile Safari/537.36\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":384,\"height\":640},\"horizontal\":{\"width\":640,\"height\":384}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"handy - nokia lumia 520 - 320x533\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (Mobile; Windows Phone 8.1; Android 4.0; ARM; Trident/7.0; Touch; rv:11.0; IEMobile/11.0; NOKIA; Lumia 520) like iPhone OS 7_0_3 Mac OS X AppleWebKit/537 (KHTML, like Gecko) Mobile Safari/537\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":320,\"height\":533},\"horizontal\":{\"width\":533,\"height\":320}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"}]"

```

<br />
<br />

 _____________________________________________________
 _____________________________________________________


<br />
<br />



# Third Party Collections

## Material Design
- Bootstrap 4 Collection: https://codepen.io/mdbootstrap/pen/LRNZBz

## Full websites
- https://codepen.io/veronicadev/details/YYvjzO
- https://codepen.io/team/webflow/pen/pvydKd

## Text
Shimmer effect: https://codepen.io/redouglas/pen/gobsm

## Lightbox:
- Lightgallery Plugin (commercial not free): https://codepen.io/sachinchoolur/pen/QjLNMM
- Single Image: https://codepen.io/gschier/pen/HCoqh
- Single Image: https://codepen.io/ongtiffany/pen/BoOeQV
- Gallery: https://codepen.io/nsom/pen/VbqLew
- Animated Gallery: https://codepen.io/designcouch/pen/DEkcf
- Gallery: https://codepen.io/svelts/pen/VYxPWW
- Grid Gallery with animation to center: https://codepen.io/ademilter/pen/ByLwwV

## Easing
- Cheat Sheet: https://easings.net/ - https://animejs.com/documentation/#pennerFunctions

## Contact Form
- https://codepen.io/jq/pen/rVVQXz
- https://codepen.io/rickyeckhardt/pen/rNVOrBL
- animation in envelope: https://codepen.io/permanentinc/pen/muFxK
- animation in envelope: https://codepen.io/asmaa-mohammed/pen/mmVaLE
- https://codepen.io/superguru/pen/aGJHA
- https://codepen.io/krisantuswanandi/pen/KxrgeZ
- https://codepen.io/mayurelbhar/pen/OPbZmy
- https://codepen.io/tutsplus/pen/ZNWQje
- https://codepen.io/melawire/pen/pGFvs
- https://codepen.io/lolwtf/pen/amVPYN
- https://codepen.io/sdras/pen/LEorev




## 403 (Forbidden) Error Page
- Typing console: https://codepen.io/leenalavanya/pen/RYqvgK
- Perspective: https://codepen.io/pgalor/pen/dqQqqx

## 404 (Not found) Error Page
- Lost astronaut:
- https://codepen.io/eroxburgh/pen/zYYyEPg
- jungle: https://codepen.io/uiswarup/pen/dyoyLOp

## 500 (Internal Server) Error Page
- https://codepen.io/Souleste/pen/QWLxPPr








## Hover
- Plugin: https://github.com/IanLunn/Hover

## UserAgent
- Database: https://developers.whatismybrowser.com/useragents/explore/operating_platform/

## Particle
- WebGL Particle Animation: https://codepen.io/kenjiSpecial/pen/vELOrM

## Table
- https://codepen.io/heypablete/pen/qdIsm

## Sidebar
- https://codepen.io/azouaoui-med/pen/wpBadb

## JSON
- JSON Viewer with Paths: http://jsonmaker.com/

## Mouse Cursor
- Guide: https://css-tricks.com/using-css-cursors/
- All avaible cursor: https://codepen.io/chriscoyier/pen/uCwfB
- Animation following cursor: https://codepen.io/tamm/pen/LIFam

## Mouse Cursor SVG Collection
- https://mega.nz/file/y3pUUCZS#NPEm6f00U2VLweB0BXLL5yf5BUU53Ndd4f0b-TvW534

## Loading screens
- https://codepen.io/ahmadbassamemran/pen/bXRPdr
- https://codepen.io/akhil_001/pen/YqBZgL
- https://tobiasahlin.com/spinkit/
- Windows 10: https://codepen.io/jenning/pen/rrkBbq
- https://codepen.io/Godwin/pen/eWBzNX
- Big Circle 3d effect: https://codepen.io/mattbhenley/pen/gQgVxG
- Loader: https://codepen.io/PicturElements/pen/ZOwkwv
- Atom Loader: https://codepen.io/dmsanchez86/details/WxRovR
- Google Loader: https://codepen.io/AmineMohamed/pen/JZxyYm

## Tabs
- https://codepen.io/RGonyeau/pen/Mvrzxx
- https://codepen.io/jdniki/pen/PzZERJ
- https://codepen.io/ejsado/pen/gPVgVv
- https://codepen.io/creativetim/pen/EgVBXa
- https://codepen.io/Danil89/pen/ONBoyG
- vertical https://codepen.io/juliepark/pen/pLMxoP
- fullscreen slideshow: https://codepen.io/pbutcher/pen/yLLKbNo
- fullscreen boxes: https://codepen.io/dtab428/pen/yYJKma
- fullscreen: https://codepen.io/team/webflow/pen/dPeVaG
- swipe with background change: https://codepen.io/federico/pen/mRovqE
- https://codepen.io/sean_codes/pen/QpoQMR
- https://codepen.io/interstellar/pen/qaRJwm



## Slider
- gradient: https://codepen.io/egrucza/pen/LEoOQZ
























## SVG Animation
- lava lamp: https://codepen.io/lukesmetham/pen/yJVwVr
- developer with notebook: https://codepen.io/jeanoliveira/pen/ObWYmY


## SVG Animations (Text)
- https://codepen.io/codecollective/pen/NqqENm
- https://codepen.io/gzmiraz/pen/XmqWWx
- https://codepen.io/mellis84/pen/JpVZNw












## Buttons General
- 3D Flip Glitch Buttons (made by me): https://codepen.io/cybert33n/pen/yXwZVx
- Button.css: https://codepen.io/kevinfan23/pen/BKbWxP
- sci-fi: https://codepen.io/jeromefarnum/details/VLjxvW
- Hold to verify: https://codepen.io/aaroniker/pen/WNNWQbM
- Button transition with 2 buttons: https://codepen.io/montechristos/pen/EPvOwJ

## Text Verification
- https://codepen.io/AlikinVV/pen/WLpRdg

## Success Button
- confetti: https://codepen.io/aaroniker/pen/bGVGNrV
- with loading: https://codepen.io/eliortabeka/pen/xOrQZA
- https://codepen.io/colinhorn/pen/KXjYXr
- https://codepen.io/guywald/details/AXwKqP
- https://codepen.io/keenanpayne/details/YmKKer
- https://codepen.io/ky0suke/pen/xwzNzp

## Delete Button
- https://codepen.io/estrepitos/pen/JAtKr

## Close Button
- Animated Close Buttons: https://codepen.io/JonasBadalic/pen/MYaMBz

## Publish Button
- Hold to verify: https://codepen.io/aaroniker/pen/BayaBpV

## Download Button
- https://codepen.io/aaroniker/pen/yRdoYN
- https://codepen.io/lalit-mohan/pen/rrEzLp
- https://codepen.io/thereyzer/pen/JqLdLr
- https://codepen.io/aaroniker/pen/vYEmery
- https://codepen.io/aaroniker/pen/KjJQER

## Add to cart Button
- https://codepen.io/aaroniker/pen/QWWXKVP

## Send Button
- https://codepen.io/aaroniker/pen/BajabVN

## Activate Button
- https://codepen.io/aaroniker/pen/ZVOrOZ

## Upload Button
- https://codepen.io/balapa/pen/VYVedm
- with pause: https://codepen.io/aaroniker/pen/QXxexJ

## Order Placed Button
- Animation with truck: https://codepen.io/aaroniker/pen/eYOVrNa
- Animation with truck v2: https://codepen.io/aaroniker/pen/oNgPOwo









## Percentage Bar
- Animated Circle: https://codepen.io/like-a-boss/pen/pgqgKq
- Multiple Charts: https://codepen.io/FilipDanic/pen/xbgbaQ

## Scroll Animation
- https://codepen.io/GreenXIII/pen/VKbNWV

## One Page
- https://codepen.io/Cutcopy/pen/LpBPLe





## Hamburger Menu Animation
- https://codepen.io/ahmadbassamemran/pen/abopOMY

## Menubar Mobile
- https://codepen.io/7ssan91/pen/dqLmpP
- https://codepen.io/raffaele-filiberti/pen/mPQqVW
- https://codepen.io/cateelderflower/pen/jwVPGd

## Menubar Desktop
- https://codepen.io/will627/pen/ehEpA
- https://codepen.io/ejsado/pen/gPVgVv
- https://codepen.io/littlesnippets/pen/BLjjVX
- https://codepen.io/littlesnippets/pen/pjKeyq
- https://codepen.io/jordiorriols/pen/OXbYKO
- Animated fullscreen: https://codepen.io/duchailu/pen/evprLy
- Fullscreen: https://codepen.io/fluxus/pen/gPWvZm
- Fullscreen: https://codepen.io/bosworthco/pen/RjBvgw
- 3D Dropdown: https://codepen.io/soulwire/pen/EKmwC
- https://codepen.io/littlesnippets/pen/gPGvLq
- https://codepen.io/yasinburakkalkan/pen/jPaXgb
- https://codepen.io/littlesnippets/pen/OMXYaG


## Sidebar Menu
- https://codepen.io/jcoulterdesign/pen/qdWxEm







## Hover
- Button hover effects with box-shadow: https://codepen.io/giana/pen/BZaGyP

## Social Media
- https://codepen.io/nouribram/pen/WNQzoOd
- https://codepen.io/daniel_wolf/pen/mJRmaQ
- https://codepen.io/FrankieDoodie/pen/dqmKrb
- 3D Cubes with Hover: https://codepen.io/gabriellewee/pen/Qdpgwx

## Converter
- Google Fonts Offline Downloader: https://google-webfonts-helper.herokuapp.com
- Image Compressor: https://imagecompressor.com
- CSS Auto Prefixer https://autoprefixer.github.io/









## Anime.js
- Animated Letters: https://tobiasahlin.com/moving-letters/
- Staggering: https://codepen.io/juliangarnier/pen/XvjWvx
- Login Box: https://codepen.io/ainalem/pen/EQXjOR
- Submit Button: https://codepen.io/andrewmillen/pen/MoKLob
- Animated Hand Signature: https://codepen.io/mellis84/pen/JpVZNw

## Animated Objects
- Animation Plugin: https://animate.style/



## Cards
- https://codepen.io/drehimself/pen/WwZrPR
- https://codepen.io/iMax723/pen/aNKQyE
- https://codepen.io/littlesnippets/pen/VvorBN
- with flip: https://codepen.io/keithpickering/pen/XJeJMv
- profile card: https://codepen.io/team/jotform/details/XWmqoMp
- profile card: https://codepen.io/littlesnippets/pen/VvOwbw
- nice border: https://codepen.io/HugoGiraudel/pen/FBbDd
- 3d flip: https://codepen.io/kharrop/pen/zBjBLx
- Multilayer with animation: https://codepen.io/jebbles/pen/MKoYya

## Typing
- Typing animation mimicking human behavior: https://codepen.io/Zhouzi/pen/JoRazP








## Error

## Success
- Modal Box animated: https://codepen.io/hynden/pen/qlsJy
- https://codepen.io/souporserious/pen/MwmXdg
- https://codepen.io/ethanthompson/pen/vpWOmN
- Modal Box not animated: https://codepen.io/iheartkode/pen/yJBBZZ
- https://codepen.io/wallaceho/details/vxLbRO
- https://codepen.io/sawyer22/pen/bdOoGX
- https://codepen.io/InaCarine/pen/RJoepK
- https://codepen.io/zhangshupi88/pen/zvWEMm
- https://codepen.io/petsto/pen/XaZRGZ
- envelope: https://codepen.io/HamishMW/pen/XJogMg

## Success & Error
- animated characters: https://codepen.io/juliepark/pen/vjMOKQ
- tooltips: https://codepen.io/veronicadev/pen/LrZaov
- https://codepen.io/MariamSalloum/pen/PBxKzd
- tooltips: https://codepen.io/prallen/details/AsECw










## Logo
- https://codepen.io/mkmueller/pen/dCEhA
- Orbit: https://codepen.io/guerreiro/pen/obhzc

## 3D
- card with mouse follow: https://codepen.io/lembitk/pen/EVmqmY
- https://codepen.io/yotman/pen/VEzXJp
- Image Carousel: https://codepen.io/hoanghien0410/pen/MMPaqm

## Newsletter
- animation mailbox: https://codepen.io/lerida/pen/BaoRRbp
- https://codepen.io/YarivFrd/pen/NXomOV

## Timeline
- Animated timeline scroll down: https://codepen.io/vincebrown/pen/BNazqL












## Sign-in
- https://codepen.io/marcobiedermann/pen/Fybpf
- https://codepen.io/mycnlz/details/aNNExj
- https://codepen.io/yildirimzlm/pen/aRjOGM
- full page with bg: https://codepen.io/carsonf92/pen/pNWGXG
- mobile: https://codepen.io/suez/pen/dPqxoM
- perspective animation: https://codepen.io/jcoulterdesign/pen/azepmX
- 3D perspective: https://codepen.io/jenning/pen/RVRYeb

## Create password
- https://codepen.io/davidkpiano/pen/WKvPBP

## Sign-up
- button sign-up: https://codepen.io/vineethtrv/pen/ZBpebQ

## Sign-in & Sign-up
- https://codepen.io/joshsorosky/pen/gaaBoB
- https://codepen.io/andytran/pen/GpyKLM
- https://codepen.io/hurick/pen/Kyrvrj
- https://codepen.io/kvaibhav01/pen/PgRgzv
- https://codepen.io/dpinnick/pen/LjdLmo
- https://codepen.io/GrandvincentMarion/pen/epEPjp
- https://codepen.io/dpinnick/pen/LjdLmo
- 3d box with all forms together: https://codepen.io/nourabusoud/pen/BxJbjJ
- fullscreen: https://codepen.io/m2creates/pen/EEvGgW
- https://codepen.io/FlorinPop17/pen/vPKWjd
- https://codepen.io/andytran/pen/RPBdgM







## Footer
- https://codepen.io/z-/details/zYxdRQy
- Animated city: https://codepen.io/uiswarup/pen/oNNMedZ
- parallax effect: https://codepen.io/maheshc/details/pCwxs
- https://codepen.io/Alioos_90/pen/VPbzpy
- https://codepen.io/magnusriga/pen/bKbWjx
- https://codepen.io/idesignsmf/pen/WgjXeo
- https://codepen.io/jilliannichols/pen/EVxLRm
- https://codepen.io/bhorsey/pen/PzPwBB
- https://codepen.io/abdelfattahbaraka/pen/rwbewP
- https://codepen.io/devdojo/pen/WNbepgJ
- https://codepen.io/Mohamed-Anwar97/pen/VwedNpR
- https://codepen.io/rhythm19/pen/RwWdKrL
- https://codepen.io/itaditya/pen/ejEYxd
- with google maps: https://codepen.io/maskit_jr/pen/EZzqYV
- https://codepen.io/nizamrobin/pen/WdoPbN
- https://codepen.io/ntoye/pen/XVGVPX
- https://codepen.io/beacrea/pen/rRWKjY
- https://codepen.io/marekzelinka/pen/VzZNVz
- https://codepen.io/salah-alden-alsalama/pen/BajWRqq
- https://codepen.io/niloydeysarkar/details/KOmbZV
- https://codepen.io/felipoliveira_/pen/WpoNgZ
- https://codepen.io/tsumetaieien/pen/rNxzgmK
- https://codepen.io/brusky/pen/yLNLMzd

## Checkbox
- https://codepen.io/alexjoffroy/pen/ORXOmR



## Testimonial
- Slider: https://codepen.io/shamim539/pen/GZPZBp
- Slider: https://codepen.io/Aashima/pen/WdQQMr
- Static: https://codepen.io/littlesnippets/pen/EVLJVa
- Static: https://codepen.io/littlesnippets/pen/yejzvR
- Static: https://codepen.io/littlesnippets/pen/yOvZPV
- Static: https://codepen.io/littlesnippets/pen/QjXVrV










## Image Carousel
- Plugin: https://owlcarousel2.github.io/OwlCarousel2/
- https://codepen.io/ccallen001/pen/bEYByd
- 3D: https://codepen.io/iamdavid/details/CDluy
- https://codepen.io/lmgonzalves/details/djEgmv
- fullscreen vertical: https://codepen.io/mxbck/pen/ERNwBy
- fullscreen: https://codepen.io/Alca/pen/VByeJd
- fullscreen vertical image distortion transition: https://codepen.io/ashthornton/details/KRQbMO
- fullscreen: https://codepen.io/lmgonzalves/pen/djEgmv

## Image Gallery
- https://codepen.io/andata/pen/pEyAGj

## Image Transitions
- https://codepen.io/sfi0zy/pen/OQOExE

















## Border Animation
- https://codepen.io/Rplus/pen/lEDBj
- https://codepen.io/uiswarup/pen/RBByzW
- https://codepen.io/littlesnippets/pen/oLajBa
- Gradient Border: https://codepen.io/mike-schultz/pen/NgQvGO




## Text animation
- https://codepen.io/team/keyframers/pen/vYNyWwQ
- https://codepen.io/KaioRocha/pen/YoEVvZ



## Popup
- https://codepen.io/melnik909/pen/QModrM

## Background Images (cc0)
- Developer on bench: https://pixabay.com/photos/work-workaholic-writer-programmer-1627703/


## Background
- bridge with clouds
- desert sun goes down svg: https://codepen.io/Unleashed-Design/pen/VNpjrW
- Gradient Collections: https://uigradients.com/#Mystic
- Animated Background: https://codepen.io/juliangarnier/pen/ZeEpgd
- Background Color Change: https://codepen.io/alexzaworski/pen/mEkvAG
- https://codepen.io/matth12377/pen/gwXBGy
- Animated Stars: https://codepen.io/shinkeo/pen/XgRqeR
- Parallax triangle figure: https://codepen.io/semenchenko/pen/JpXVgG
- Parallax Mouse follow with stars bg: https://codepen.io/ybprogrammer/pen/PGNBXJ
- Animated waves: https://codepen.io/miguelog/pen/amoWgy
- Endless horizontal Loop of Image: https://codepen.io/asfarmed/pen/cfslr
- Moving circles and squares: https://codepen.io/tokyoweb/pen/ZjdYVj
- Waves bottom: https://codepen.io/abelhancock/pen/aKxmLY
- Moving Logos on servers: https://codepen.io/koshik-ojha/pen/LXzXyx
- Moving Circles: https://codepen.io/Nathanmc4pg/pen/GdKLdY
- Solar System: https://codepen.io/kowlor/pen/ZYYQoy
- Spread: https://codepen.io/roboshoes/pen/ydipI
- Animated Person: https://codepen.io/yahiarefaiea/pen/xyNWQq
- Animated stars fall down from sky: https://codepen.io/chriscourses/pen/PzONKR
- Planet bg: https://codepen.io/carsonf92/pen/pNWGXG
- planet bg v2: https://codepen.io/MoodyBoles/pen/KVodmp
- Three.js mutating field: https://codepen.io/Samsy/pen/emWppX

## Animated Gradient Background
```css

/* version 1 - multicolor*/
background: grey; /*fallback for older browsers*/
background: linear-gradient(-45deg, #f57f19, #e0366deb, #f57f19, #e0366deb, #195bf573, #000000, #00000073, #000000eb);
background-size: 400% 400%;
-webkit-animation: Gradient 43s ease infinite;
-moz-animation: Gradient 43s ease infinite;
animation: Gradient 43s ease infinite;

/* version 2 - transparent purple */
background: grey; /*fallback for older browsers*/
background: linear-gradient(-45deg, #72307aba, #000000, #000000, #000000, #72307aba, #0000007d, #000000, #000000);
background-size: 400% 400%;
-webkit-animation: Gradient 630s ease infinite;
-moz-animation: Gradient 630s ease infinite;
 animation: Gradient 630s ease infinite;

/*version 3 - grey to blue*/
background: grey; /*fallback for older browsers*/
background: linear-gradient(-45deg, #000000eb, #1d60d2f2, #000000, #383838, #000000f7, #383838);
background-size: 400% 400%;
-webkit-animation: Gradient 120s ease infinite;
-moz-animation: Gradient 120s ease infinite;
animation: Gradient 120s ease infinite;

/* version 4 - orange to purple to yellow - looks good with black bg */
 background: grey; /*fallback for older browsers*/
 background: linear-gradient(-45deg, #ef6706, #e2c70a, #ffc404, #f81a62, #e0366d, #f57f19, #f27a1c);
 background-size: 400% 400%;
 -webkit-animation: Gradient 63s ease infinite;
 -moz-animation: Gradient 63s ease infinite;
 animation: Gradient 63s ease infinite;


@-webkit-keyframes Gradient {
	0% {
		background-position: 0% 50%
	}
	50% {
		background-position: 100% 50%
	}
	100% {
		background-position: 0% 50%
	}
}

@-moz-keyframes Gradient {
	0% {
		background-position: 0% 50%
	}
	50% {
		background-position: 100% 50%
	}
	100% {
		background-position: 0% 50%
	}
}

@keyframes Gradient {
	0% {
		background-position: 0% 50%
	}
	50% {
		background-position: 100% 50%
	}
	100% {
		background-position: 0% 50%
	}
}


```

<br />
<br />

 _____________________________________________________
 _____________________________________________________


<br />
<br />


