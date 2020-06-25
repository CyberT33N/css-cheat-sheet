# CSS Cheat Sheet
CSS Cheat Sheet with the most needed stuff..



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
margin: auto;
width: 200px;

/* Method #1 */
position: fixed;
top: 50%;
left: 50%;
transform: translate(-50%, -50%);
```  




# Two DIV next to each other
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


