e
# CSS Cheat Sheet   (つ◉益◉)つ  
CSS Cheat Sheet with the most needed stuff..









<br><br>
 _____________________________________________________
 _____________________________________________________
<br><br>


# CSS-Referenz

<br><br>

<details><summary>Click to expand..</summary>


#  @scope Regel

## Überblick
Die `@scope` Regel in CSS ermöglicht das Scoping von Stilen auf bestimmte Teile des DOMs. Sie ist nützlich, um Styles auf eine begrenzte Gruppe von Elementen anzuwenden, ohne dass diese Styles das gesamte Dokument beeinflussen.

## Syntax
```css
@scope (<selector>) {
  /* Styles für Elemente innerhalb des Scopes */
}
```


Beispiel 1: Scoping innerhalb eines Containers
```css

@scope (.container) {
  /* Alle <p>-Tags innerhalb des .container werden rot */
  p {
    color: red;
  }
}
```

Beispiel 2: Scoping mit einem Nachfolgenden Selektor
```css

@scope (.container) to (.content) {
  /* Alle <p>-Tags innerhalb des .container, aber vor .content werden grün */
  p {
    color: green;
  }
}
```

Beispiel 3: Kombiniertes Scoping
```css

@scope (.container) {
  @scope (.inner-box) {
    /* Nur <p>-Tags innerhalb von .inner-box, das innerhalb von .container ist, werden blau */
    p {
      color: blue;
    }
  }
}
```

Beispiel 4: Negation innerhalb des Scopes
```css

@scope (.container) {
  /* Alles außer <p>-Tags innerhalb von .container wird gelb */
  :not(p) {
    color: yellow;
  }
}
```

Wichtige Punkte

    Die @scope Regel ist experimentell und noch nicht in allen Browsern vollständig unterstützt.
    to kann verwendet werden, um den Scope weiter einzugrenzen.
    Der Scope kann verschachtelt werden, um noch spezifischere Stile zu definieren.


Browserunterstützung

    Chrome: Experimentelle Unterstützung aktivierbar via Flags.
    Firefox: Noch keine Unterstützung.
    Safari: Experimentelle Unterstützung aktivierbar via Flags.


Hinweis: Überprüfe immer die aktuelle Browserunterstützung, da sich diese schnell ändern kann.

</details>




















<br><br>
 _____________________________________________________
 _____________________________________________________
<br><br>


# API

<br><br>

<details><summary>Click to expand..</summary>


# CSS Houdini: Was ist das? (+ Beispiele)

CSS Houdini ist eine Sammlung von **APIs**, die Entwicklern ermöglichen, die Grenzen von CSS zu überschreiten, indem sie direkt in den Browser-Rendering-Prozess eingreifen. Damit kannst du eigene Stile, Layouts und Animationen erstellen, die nativ vom Browser verarbeitet werden.

---

## Beispiele für CSS Houdini

### 1. **Paint API**: Benutzerdefinierte Hintergründe erstellen
Mit der Paint API kannst du eigene Hintergrundmuster oder Grafiken zeichnen.

#### Beispiel: Streifenmuster als Hintergrund
```javascript
// paint-worklet.js
class StripedBackground {
  paint(ctx, size, properties) {
    const stripeWidth = 10;
    ctx.fillStyle = 'blue';
    for (let x = 0; x < size.width; x += stripeWidth * 2) {
      ctx.fillRect(x, 0, stripeWidth, size.height);
    }
  }
}
registerPaint('striped-bg', StripedBackground);
```

In deinem CSS:
```css
/* CSS: Stripe-Background aktivieren */
@paint-worklet addModule('paint-worklet.js');

div {
  background: paint(striped-bg);
  width: 200px;
  height: 100px;
}
```

---

### 2. **Properties and Values API**: Eigene CSS-Variablen definieren
Hier kannst du benutzerdefinierte CSS-Eigenschaften mit Standardwerten und Typen erstellen.

#### Beispiel: Benutzerdefinierte Eigenschaft "theme-color"
```javascript
CSS.registerProperty({
  name: '--theme-color',
  syntax: '<color>',
  inherits: false,
  initialValue: 'black',
});
```

In deinem CSS:
```css
/* CSS: Verwende die registrierte Eigenschaft */
div {
  background-color: var(--theme-color);
}
```

In deinem JavaScript:
```javascript
// Ändere die Eigenschaft dynamisch
document.querySelector('div').style.setProperty('--theme-color', 'blue');
```

---

### 3. **Animation Worklet**: Komplexe Animationen steuern
Mit der Animation Worklet API kannst du benutzerdefinierte Animationen erstellen, die besser performen.

#### Beispiel: Physik-basierte Animation
```javascript
// animation-worklet.js
class BounceAnimation {
  constructor() {
    this.time = 0;
  }
  animate(currentTime, effect) {
    this.time += 0.1;
    const offset = Math.abs(Math.sin(this.time));
    effect.localTime = offset * 1000; // Animationszeit steuern
  }
}
registerAnimator('bounce', BounceAnimation);
```

In deinem CSS:
```css
/* Animation Worklet aktivieren */
@keyframes bounce {
  from { transform: translateY(0); }
  to { transform: translateY(-50px); }
}
div {
  animation: bounce 1s infinite alternate;
}
```

---

### 4. **Layout API**: Eigene Layouts erstellen
Die Layout API erlaubt dir, komplett neue Layout-Methoden zu definieren.

#### Beispiel: Ein einfaches "Stacked" Layout
```javascript
class StackedLayout {
  *layout(children, edges, constraints, styleMap) {
    let y = edges.inlineStart;
    for (const child of children) {
      const childFragment = yield child.layoutNextFragment();
      childFragment.inlineOffset = edges.inlineStart;
      childFragment.blockOffset = y;
      y += childFragment.blockSize;
    }
  }
}
registerLayout('stacked', StackedLayout);
```

In deinem CSS:
```css
/* Layout aktivieren */
@layout-worklet addModule('layout-worklet.js');

.container {
  display: layout(stacked);
}
```

---

## Fazit
CSS Houdini gibt dir die Macht, Dinge zu erstellen, die mit normalem CSS nicht möglich sind. Egal ob benutzerdefinierte Hintergründe, bessere Animationen oder neue Layouts – Houdini bietet dir die nötigen Tools.

Mehr Infos und Beispiele findest du [hier](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Houdini).


</details>









<br><br>
 _____________________________________________________
 _____________________________________________________
<br><br>


# CSS Properties

<br><br>

<details><summary>Click to expand..</summary>










# Pseudo Class

<details><summary>Click to expand..</summary>

## :has
- The functional :has() CSS pseudo-class represents an element if any of the relative selectors that are passed as an argument match at least one element when anchored against this element. This pseudo-class presents a way of selecting a parent element or a previous sibling element with respect to a reference element by taking a relative selector list as an argument.
- https://developer.mozilla.org/en-US/docs/Web/CSS/:has
```css
/* Selects an h1 heading with a
paragraph element that immediately follows
the h1 and applies the style to h1 */
h1:has(+ p) {
  margin-bottom: 0;
}

```




<br><br>
<br><br>

## ::before & ::after

<br><br>

### Access via JS
```javascript
getComputedStyle(document.querySelector('span.search-box'), '::after').getPropertyValue('content');
```














<br><br>
<br><br>

# :is()
- https://github.com/CyberT33N/css-cheat-sheet/edit/master/README.md
- Helps simplify complex selectors. It accepts a list of selectors and applies styles if any match. It's specificity-aware.
- **Was es macht:** Vereinfacht komplexe Selektoren. Es akzeptiert eine Liste von Selektoren und fügt die Styles an jedes Element an, das mit einem der Selektoren übereinstimmt.  
- **Besonderheit:** Die **Spezifität** von `:is()` wird von dem **spezifischsten Selektor** in der Liste bestimmt.

#### Beispiel:
```css
:is(h1, h2, h3) {
  color: red;
}
```
- **Wirkung:** Alle `h1`, `h2` und `h3` werden rot.  
- **Spezifität:** Die Spezifität ist so hoch wie der spezifischste Selektor in der Liste (in diesem Fall `h1`, `h2`, `h3`).

##### Anwendung bei verschachtelten Selektoren:
```css
article :is(h1, h2, h3) {
  text-transform: uppercase;
}
```
- **Wirkung:** Wandelt alle Überschriften (`h1`, `h2`, `h3`) **innerhalb** eines `<article>` in Großbuchstaben um.






<br><br>
<br><br>

# :where()
- https://developer.mozilla.org/de/docs/Web/CSS/:where
- Die :where() CSS Pseudoklasse Funktion nimmt eine Selektorliste als Argument und wählt jedes Element aus, das durch einen der Selektoren in dieser Liste ausgewählt werden kann.
- **Was es macht:** Funktioniert ähnlich wie `:is()`, aber **ohne Spezifität**. Die Selektoren in `:where()` haben immer eine Spezifität von `0`.  
- **Nutzen:** Es eignet sich besonders gut, um Standard-Styling zu definieren, das leicht überschrieben werden kann.

#### Beispiel:
```css
:where(h1, h2, h3) {
  margin: 0;
  color: gray;
}
```
- **Wirkung:** Entfernt den Außenabstand (margin) und macht die Schrift grau für alle `h1`, `h2`, und `h3`.  
- **Spezifität:** Kann durch **jede andere Regel** leicht überschrieben werden.

##### Anwendung bei komplexen Strukturen:
```css
:where(nav, header, footer) :where(a) {
  color: blue;
  text-decoration: none;
}
```
- **Wirkung:** Alle Links (`<a>`) **innerhalb von `nav`, `header`, oder `footer`** bekommen eine blaue Schrift und keine Unterstreichung.  



# **Vergleich von `:is()` und `:where()`**
| Eigenschaft        | `:is()`                                   | `:where()`                                |
|--------------------|-------------------------------------------|-------------------------------------------|
| **Spezifität**     | Von dem **spezifischsten Selektor** abhängig | Immer **0**                              |
| **Überschreibbarkeit** | Schwerer zu überschreiben                | Leicht zu überschreiben                   |
| **Nutzen**         | Für komplexe, spezifische Selektoren       | Für Standard-Styling ohne Konflikte       |

---

### Kombinierte Verwendung:
```css
:is(section, article) :where(h1, h2, h3) {
  font-size: 2rem;
  color: green;
}
```
- **Wirkung:** Überschriften (`h1`, `h2`, `h3`) **innerhalb von `section` oder `article`** bekommen grüne Farbe und eine Schriftgröße von 2rem.
- **Spezifität:** Wird von `:is()` bestimmt, aber `:where()` selbst trägt nichts zur Spezifität bei.




</details>














# view()
- https://developer.mozilla.org/en-US/docs/Web/CSS/animation-timeline/view
- https://javascript.plainenglish.io/finally-a-better-way-to-handle-scroll-animations-ac3f4fc1bc1e
```css
@keyframes fadeInOut {
  0% {
    opacity: 0;
    scale: 0.5;
    transform: translateX(100%);
  }
  50% {
    opacity: 1;
    scale: 1;
    transform: translateX(0);
  }
  100% {
    opacity: 0;
    scale: 0.5;
    transform: translateX(100%);
  }
}

.fade-in-out {
  animation: fadeInOut linear;
  animation-timeline: view();
  animation-range: entry exit;
}
```





<br><br>

# scroll-snap-type


So first, you need to set up a scroll-snap-type for the parent container. To make it work like in YouTube Shorts, we will set it to y mandatory.
```css
.scroll-container {
  display: flex;
  flex-direction: column;
  overflow-y: scroll;
  scroll-snap-type: y mandatory;
  width: 300px;
  height: 80%;
  background-color: #ddd;
  padding: 20px;
  box-sizing: border-box;
  scroll-padding: 10px;
}
```

That means the scroll container snaps in its vertical axis only and the content must snap to a snap position if it isn’t currently scrolled. Check MDN Docs for the detailed explanation of each possible value for this property.

And for each of the scrolled items we just need to provide a snap position of the item within its snap area. In other words, do we want the item to be snapped to the top (start), center or to the bottom (end). It’s possible thanks to the scroll-snap-align property:

```css
.scroll-item {
  scroll-snap-align: start;
}
```

Take a look at the demo, it’s really very cool feature and using CSS only:
- https://codepen.io/bogdanfromkyiv/pen/zYVjwme







<br><br>


# light-dark()
- https://developer.mozilla.org/en-US/docs/Web/CSS/color_value/light-dark
- The light-dark() CSS <color> function enables setting two colors for a property - returning one of the two colors options by detecting if the developer has set a light or dark color scheme or the user has requested light or dark color theme - without needing to encase the theme colors within a prefers-color-scheme media feature query. Users are able to indicate their color-scheme preference through their operating system settings (e.g. light or dark mode) or their user agent settings. The light-dark() function enables providing two color values where any <color> value is accepted. The light-dark() CSS color function returns the first value if the user's preference is set to light or if no preference is set and the second value if the user's preference is set to dark. 



<br><br>


# align-content
- https://www.w3schools.com/cssref/css3_pr_align-content.php

The align-content property specifies how flex lines are distributed along the cross axis in a flexbox container.

In flexbox layout, the main axis is in the flex-direction (default is 'row', horizontal), and the cross axis is perpendicular to the main axis (default is 'column', vertical).

Tip: Use the justify-content property to align the items on the main axis (horizontally).

Note: The align-content property can also be used on a grid container to align grid items in the block direction. For pages in English, block direction is downward and inline direction is left to right.
```
div {
  width: 70px;
  height: 300px;
  border: 1px solid #c3c3c3;
  display: flex;
  flex-wrap: wrap;
  align-content: center;
}
```



</details>















<br><br>
 _____________________________________________________
 _____________________________________________________
<br><br>

# Units


# dvh, lvh & svh
https://dev.to/frehner/css-vh-dvh-lvh-svh-and-vw-units-27k4





















<br><br>
 _____________________________________________________
 _____________________________________________________
<br><br>



# CSS Flexbox vs. Grid: Wann du was verwenden solltest

<details><summary>Click to expand..</summary>

CSS bietet zwei leistungsstarke Layout-Tools: **Flexbox** und **Grid**. Beide haben ihre Stärken, aber sie sind für unterschiedliche Zwecke optimiert. Hier ist ein Überblick, um zu entscheiden, wann du welches verwenden solltest.

## CSS Grid: Zwei-dimensionale Layouts
**Grid** ist ideal für **komplexe, zweidimensionale Layouts**, bei denen sowohl Reihen als auch Spalten gesteuert werden müssen.

### Vorteile von Grid:
- **Präzise Kontrolle** über Zeilen und Spalten.
- **Überlappende Elemente** einfach gestalten.
- **Komplexe Layouts** (Dashboards, Hauptinhaltsbereiche) einfach definieren.

### Beispiel:
```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: auto;
  gap: 20px;
}
```

Verwendung: Hauptlayouts wie Seitenraster, Galerien oder Dashboards.

---

## CSS Flexbox: Ein-dimensionale Layouts
**Flexbox** ist für **einfache, ein-dimensionale Layouts** optimiert. Es hilft, Elemente in einer Zeile oder Spalte flexibel auszurichten.

### Vorteile von Flexbox:
- **Einfache Ausrichtung** entlang einer Achse.
- **Dynamische Größen** und gleichmäßige Verteilung von Platz.
- Perfekt für **Navigationen** oder **mobile Layouts**.

### Beispiel:
```css
.container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
```

Verwendung: Navigationselemente, Button-Gruppen, Spaltenlayouts für mobile Geräte.

---

## Wann Grid, wann Flexbox?
| **Szenario**                         | **Verwenden**  |
|--------------------------------------|----------------|
| Layout mit Reihen und Spalten        | **Grid**       |
| Elemente in einer Linie ausrichten   | **Flexbox**    |
| Genaue Platzierung von Elementen     | **Grid**       |
| Dynamische Verteilung von Platz      | **Flexbox**    |

---

## Hybridansatz: Das Beste aus beiden Welten
Manchmal lohnt es sich, **Grid** für die Struktur und **Flexbox** für die Ausrichtung innerhalb von Zellen zu kombinieren.

### Best Practices:
1. **Grid** für das Hauptlayout.
2. **Flexbox** für die Ausrichtung von Elementen innerhalb der Zellen.
3. **Kommentiere deinen Code**, um Klarheit zu bewahren.

```css
.container {
  display: grid;
  grid-template-columns: 1fr 2fr;
}

.item {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

---

## Fazit
Verstehe die Stärken von Grid und Flexbox, um je nach Anforderung das passende Tool zu wählen. Für maximale Flexibilität kann eine Kombination beider Techniken die optimale Lösung sein.

### Zusätzliche Ressourcen
- [MDN: CSS Grid Layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout)
- [CSS-Tricks: A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

</details>







<br><br>
<br><br>



















# Flex

<details><summary>Click to expand..</summary>


# Snippets

<br><br>

## Align

<br><br>

## Align 2 images next to each toher
```
<div style="display: flex; justify-content: center; align-items: center; gap: 10px;">
  <a href="https://www.linkedin.com/in/dennis-dd">
    <img width="30" src="https://upload.wikimedia.org/wikipedia/commons/e/e9/Linkedin_icon.svg" alt="LinkedIn"/>
  </a>
  <a href="https://www.xing.com/profile/Dennis_Demand05690">
    <img width="30" src="https://upload.wikimedia.org/wikipedia/fr/d/d2/Xing_logo.png" alt="Xing"/>
  </a>
</div>
```


<br><br>

## Image right and text left
```html
<div style="display: flex; justify-content: flex-start; align-items: flex-start; gap: 10px;">
    <div style="flex: 1; text-align: left;">
        <div style="font-size: 1.5em;">
            <strong>★ SUPPORT ★</strong><br>
            ✅ 𝘞𝘰𝘳𝘬 𝘛𝘪𝘮𝘦 𝟐𝟒/𝟕 🕜<br>
            ✅ 𝙁𝙍𝙀𝙀 𝙇𝙄𝙁𝙀𝙏𝙄𝙈𝙀 𝘚𝘶𝘱𝘱𝘰𝘳𝘵 💭<br>
        </div>
        <br>
        <div style="font-size: 1.5em;">
            <strong>★ SERVICE ★</strong><br>
            ✅ 𝐏𝐫𝐨𝐟𝐞𝐬𝐬𝐢𝐨𝐧𝐚𝐥 𝘚𝘰𝘧𝘵𝘸𝘢𝘳𝘦 🤖<br>
            ✅ 𝟏𝟎 𝙮𝙚𝙖𝙧𝙨 𝙤𝙛 𝙚𝙭𝙥𝙚𝙧𝙞𝙚𝙣𝙘𝙚 ☕<br>
            ✅ 𝐖𝐢𝐧𝐝𝐨𝐰𝐬, 𝐌𝐀𝐂 & 𝐋𝐢𝐧𝐮𝐱 💻<br>
            ✅ 𝘛𝘩𝘦 𝙘𝙝𝙚𝙖𝙥𝙚𝙨𝙩 𝙥𝙧𝙞𝙘𝙚 𝘧𝘰𝘳 𝘤𝘰𝘮𝘱𝘭𝘦𝘹 𝘗𝘳𝘰𝘣𝘭𝘦𝘮𝘴 💲<br>
        </div>
    </div>
    
    <img style="width: 50%; height: auto;" alt="fullstack services" src="https://i.imgur.com/Tn8Vyfd.png" />
</div>

<style>
    @media (max-width: 768px) {
        div > div {
            font-size: 1.2em; /* Slightly smaller font size for smaller screens */
        }
    }
    @media (max-width: 480px) {
        div > div {
            font-size: 1em; /* Even smaller for mobile devices */
        }
    }
</style>

```


</details>










<br><br>
 _____________________________________________________
 _____________________________________________________
<br><br>

# grid

<details><summary>Click to expand..</summary>


# Build Dynamic, Responsive Grids with `repeat()` and `minmax()`

Mit den Funktionen **`repeat()`** und **`minmax()`** kannst du **responsive** und **dynamische Grids** erstellen, die sich automatisch an den verfügbaren Platz anpassen.

## Erklärung:
1. **`repeat()`**:
   - Wiederholt eine Spalte oder Zeile mehrere Male.
   - Syntax: `repeat(<Anzahl>, <Wert>)` oder `repeat(auto-fit/auto-fill, <Wert>)`.

2. **`minmax()`**:
   - Legt den **Mindest- und Höchstwert** für eine Spalte oder Zeile fest.
   - Syntax: `minmax(<min>, <max>)`.

### Beispiel: Dynamisches Grid mit `repeat()` und `minmax()`
```css
.container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: 16px;
}
```

### Was passiert hier?
- **`repeat(auto-fit, minmax(150px, 1fr))`:**
  - **`auto-fit`**: Passt die Anzahl der Spalten dynamisch an, basierend auf dem verfügbaren Platz.
  - **`minmax(150px, 1fr)`**: 
    - Die Breite jeder Spalte beträgt mindestens **150px**.
    - Die maximale Breite einer Spalte füllt den verfügbaren Platz gleichmäßig aus (`1fr`).

- **`gap: 16px;`**: Fügt Abstände von **16px** zwischen den Grid-Elementen hinzu.

---

## Vorteile:
- **Flexibilität**: Das Grid passt sich automatisch an verschiedene Bildschirmgrößen an.
- **Einfachheit**: Weniger Media Queries erforderlich.
- **Responsives Design**: Perfekt für mobile und Desktop-Layouts.

---

## Anwendung:
- **Galerien**: Bilder mit flexibler Größe.
- **Kartenlayouts**: Produktübersichten, Blog-Posts.
- **Dashboard-Designs**: Widgets, die sich dynamisch anpassen.

---

### Weiteres Beispiel: Unterschied zwischen `auto-fit` und `auto-fill`
#### `auto-fit`:
Spalten passen sich dynamisch an und füllen den gesamten Platz aus, selbst wenn weniger Inhalte vorhanden sind.

```css
grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
```

#### `auto-fill`:
Spalten bleiben in ihrer festen Breite, auch wenn sie nicht den gesamten Platz ausfüllen.

```css
grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
```

---

## Fazit:
Mit **`repeat()`** und **`minmax()`** kannst du moderne, anpassungsfähige Grids erstellen, die sowohl ästhetisch ansprechend als auch funktional sind. Sie sind ein Must-Have-Tool für responsives Webdesign!




<br><br>
<br><br>



## seamless responsive photo grid (https://css-tricks.com/seamless-responsive-photo-grid/)
```html
<section id="photos">
  <img src="images/cat-1.jpg" alt="Cute cat">
  <img src="images/cat-2.jpg" alt="Serious cat">
  ...
</section>
```
```css
#photos {
  /* Prevent vertical gaps */
  line-height: 0;
   
  -webkit-column-count: 5;
  -webkit-column-gap:   0px;
  -moz-column-count:    5;
  -moz-column-gap:      0px;
  column-count:         5;
  column-gap:           0px;  
}

#photos img {
  /* Just in case there are inline attributes */
  width: 100% !important;
  height: auto !important;
}



@media (max-width: 1200px) {
  #photos {
  -moz-column-count:    4;
  -webkit-column-count: 4;
  column-count:         4;
  }
}
@media (max-width: 1000px) {
  #photos {
  -moz-column-count:    3;
  -webkit-column-count: 3;
  column-count:         3;
  }
}
@media (max-width: 800px) {
  #photos {
  -moz-column-count:    2;
  -webkit-column-count: 2;
  column-count:         2;
  }
}
@media (max-width: 400px) {
  #photos {
  -moz-column-count:    1;
  -webkit-column-count: 1;
  column-count:         1;
  }
}
```

<br><br>

## 3 columns
```css
.grid-container {
  display: grid;
  grid-template-columns: auto auto auto;
  padding: 10px;
}
.grid-item {
  background-color: rgba(255, 255, 255, 0.8);
  border: 1px solid rgba(0, 0, 0, 0.8);
  padding: 20px;
  font-size: 30px;
  text-align: center;
}
```

<br>

```html
<div class="grid-container">
  <div class="grid-item">1</div>
  <div class="grid-item">2</div>
  <div class="grid-item">3</div>  
  <div class="grid-item">4</div>
  <div class="grid-item">5</div>
  <div class="grid-item">6</div>  
  <div class="grid-item">7</div>
  <div class="grid-item">8</div>
  <div class="grid-item">9</div>  
</div>
```


</details>







































<br><br>
 _____________________________________________________
 _____________________________________________________
<br><br>

# :nth-child()
https://www.w3schools.com/cssref/sel_nth-child.asp
























<br><br>
 _____________________________________________________
 _____________________________________________________
<br><br>

# Performance 

<details><summary>Click to expand..</summary>

- https://web.dev/lighthouse-performance/



<br>
<br>

## content-visibility (https://web.dev/content-visibility/)
```css
content-visibility: auto;
```

```javascript
if ("content-visibility" in document.body.style) alert("The property is supported");
else alert("The property is NOT supported");
```
<br>
<br>

## Ensure text remains visible during webfont load
- https://web.dev/font-display/

```css
/*Use swap*/
<link href="https://fonts.googleapis.com/css?family=Roboto:400,700&display=swap" rel="stylesheet">
@import url(https://fonts.googleapis.com/css?family=Alex+Brush&display=swap);
```
<br>
<br>

## SVG Sprite
- https://github.com/svgstore/svgstore
- https://svgsprit.es/ **Online generator**
- https://www.npmjs.com/package/svg-sprite-generator







<br>
<br>

## Alternative to box-shadow transition
- Have you ever been using a Material Design web app and thought “this just feels slow”? It might be because, well, it was. Material Design relies heavily on shadows to indicate depth and relationships. As AirBnB discovered, box shadows are slow. To make matters worse, animating shadow blur to make an element feel like it’s moving forward and backward is a design pattern seen all over the place. Shadows cause a repaint on every frame they’re changed, so shadow transitions are incredibly slow.
- https://codepen.io/tribex/pen/ZxXJoO

```css
/* The old, slow way. */
.slow-transition {
  box-shadow: 0 0 10px 0 rgba(0, 0, 0, 0.3);
  transition: box-shadow 500ms;
}

.slow-transition:hover {
  box-shadow: 0 10px 50px 0 rgba(0, 0, 0, 0.5);
}

/* The fast, new way! */
.fast-transition {
  position: relative; /* For positioning the pseudo-element */
  box-shadow: 0 0 10px 0 rgba(0, 0, 0, 0.3);
}

.fast-transition::before {
  /* Position the pseudo-element. */
  content: ' ';
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;

  /* Create the box shadow at expanded size. */
  box-shadow: 0 10px 50px 0 rgba(0, 0, 0, 0.5);

  /* Hidden by default. */
  opacity: 0;
  transition: opacity 500ms;
}

.fast-transition:hover::before {
  /* Show the pseudo-element on hover. */
  opacity: 1;
}
```








<br>
<br>

## Load images only when in viewport
```html
<img class="layerone-img-ich2" data-src="img/ich-min.png"/>
```
```javascript
  // when you reach the layer of the image load it manually by changing data-src to src
  $('.layerone-img-ich2').attr( 'src', $('.layerone-img-ich2').attr( 'data-src' ) );
  document.querySelector('.layerone-img-ich2').onload = function(e){
  console.log( 'image loaded..' );
      // code, run after image load
   }
```

## Images
- Convert images to .webp

<br>
<br>


## HTTP 2
- https://web.dev/uses-http2/?utm_source=lighthouse&utm_medium=devtools

<br>
<br>



<br>
<br>

## Minify

#### Server Side
```bash
# https://github.com/tdewolff/minify
sudo apt-get install minify
minify -o index-min.html index.html

#You can also give directories as input, and these directories can be minified recursively.

#Minify files in the current working directory to out/ (no subdirectories):
minify -o out/ .

# Minify files recursively in src/:
minify -r -o out/ src

#Minify only javascript files in src/:
minify -r -o out/ --match=\.js src
```

</details>






























<br><br>
 _____________________________________________________
 _____________________________________________________
<br><br>

# Media Queries (https://gist.github.com/bartholomej/8415655)

<details><summary>Click to expand..</summary>

```css
/*------------------------------------------
  Responsive Grid Media Queries - 1280, 1024, 768, 480
   1280-1024   - desktop (default grid)
   1024-768    - tablet landscape
   768-480     - tablet
   480-less    - phone landscape & smaller
--------------------------------------------*/

/*------------------------------------------*/

@media all and (min-width: 1921px) {

}

@media all and (min-width: 1601px) and (max-width: 1920px) {

}

@media all and (min-width: 1441px) and (max-width: 1600px) {
    .content .iframe {
        width: 100%;
    }
}
@media all and (min-width: 1441px) {
    .content .iframe {
        width: 100%;
    }
}

@media all and (min-width: 1281px) and (max-width: 1440px) {

}

@media all and (min-width: 1025px) and (max-width: 1280px) {
    .content .iframe {
        width: 125%;
        transform: translate(-5em, -4em);
    }

    .content {
        max-width: 80%;
    }
}

@media all and (min-width: 769px) and (max-width: 1024px) {
    .content {
        max-width: 75%;
    }

    .content .iframe {
        width: 170%;
        transform: translate(-8em, -7em);
    }

    nav {
        padding: 0;
    }

    form {
        width: 30em;
    }
}

@media all and (min-width: 481px) and (max-width: 768px) { }

@media all and (max-width: 480px) { }

/*------------------------------------------
  Foundation Media Queries
   http://foundation.zurb.com/docs/media-queries.html
--------------------------------------------*/

/* Small screens - MOBILE */
@media only screen { } /* Define mobile styles - Mobile First */

@media only screen and (max-width: 40em) { } /* max-width 640px, mobile-only styles, use when QAing mobile issues */

/* Medium screens - TABLET */
@media only screen and (min-width: 40.063em) { } /* min-width 641px, medium screens */

@media only screen and (min-width: 40.063em) and (max-width: 64em) { } /* min-width 641px and max-width 1024px, use when QAing tablet-only issues */




/* Portrait */
@media screen and (orientation:portrait) { /* Portrait styles here */ }
/* Landscape */
@media screen and (orientation:landscape) { /* Landscape styles here */ }


/* CSS for iPhone, iPad, and Retina Displays */

/* Non-Retina */
@media screen and (-webkit-max-device-pixel-ratio: 1) {
}

/* Retina */
@media only screen and (-webkit-min-device-pixel-ratio: 1.5),
only screen and (-o-min-device-pixel-ratio: 3/2),
only screen and (min--moz-device-pixel-ratio: 1.5),
only screen and (min-device-pixel-ratio: 1.5) {
}

/* iPhone Portrait */
@media screen and (max-device-width: 480px) and (orientation:portrait) {
}

/* iPhone Landscape */
@media screen and (max-device-width: 480px) and (orientation:landscape) {
}

/* iPad Portrait */
@media screen and (min-device-width: 481px) and (orientation:portrait) {
}

/* iPad Landscape */
@media screen and (min-device-width: 481px) and (orientation:landscape) {
}



/*------------------------------------------
  Live demo samples
   - http://andrelion.github.io/mediaquery/livedemo.html
--------------------------------------------*/
```

## Orientation
```css
@media all and (max-width: 1024px) and (min-height: 1025px) and (orientation: portrait)  { /*..*/ }
```

## Prevent sticky hover on touch devices
```css
/*Method #1*/

/*This media query indicates that styles will work on browsers that not emulate :hover so it will NOT work on touch browsers.*/
@media (hover: hover) and (pointer: fine) {
    /* css hover class/style */
}

/*Method #2*/
.myhoveredclass {
    background-color:green;
}
.myhoveredclass:hover {
    background-color:red;
}
@media screen and (-webkit-min-device-pixel-ratio:0) {
    .myhoveredclass:hover, .myhoveredclass:active, .myhoveredclass:focus {
        background-color:green;
    }
}
```

```javascript
// method #3
$("#elementwithhover").click(function() { 
  // code that makes element or parent slide or otherwise move out from under mouse. 

  $(this).clone(true).insertAfter($(this));
  $(this).remove();
});
```

## Device Pixel Ratio
```css
/* iPhone 6 landscape */
@media only screen and (min-device-width: 375px)
  and (max-device-width: 667px)
  and (orientation: landscape)
  and (-webkit-min-device-pixel-ratio: 2)
  {
  /* Your CSS */
  }

/* iPhone 6 portrait */
@media only screen
  and (min-device-width: 375px)
  and (max-device-width: 667px)
  and (orientation: portrait)
  and (-webkit-min-device-pixel-ratio: 2)
  {
  /* Your CSS */
  }


/* iPhone 6 Plus landscape */
@media only screen
  and (min-device-width: 414px)
  and (max-device-width: 736px)
  and (orientation: landscape)
  and (-webkit-min-device-pixel-ratio: 3)
  {
  /* Your CSS */
  }


/* iPhone 6 Plus portrait */
@media only screen 
  and (min-device-width: 414px) 
  and (max-device-width: 736px) 
  and (orientation: portrait) 
  and (-webkit-min-device-pixel-ratio: 3)
  {
  /* Your CSS */
  }



/* iPhone 6 and 6 Plus */
@media only screen
  and (max-device-width: 640px),
  only screen and (max-device-width: 667px),
  only screen and (max-width: 480px)
  {
  /* Your CSS */
  }
```


</details>




























<br>
<br>
 _____________________________________________________
 _____________________________________________________
<br>
<br>


# Video

<details><summary>Click to expand..</summary>

# Fit video into div

Option 1:
```
<video style="width: 650px; height: 362px; object-fit: cover;" autoplay muted loop playsinline preload="metadata" class="img-fluid rounded-1 img-fadeIn-4">
<source src="./assets/videos/2.webm" type="video/webm">
<source src="./assets/videos/2.mp4" type="video/mp4">
Your Browser does not support this format.
</video>
```


Option 2:
I was just in a similar situation, came to a solution not already mentioned:

`html` and `body` filling the viewport, `#header` and `#footer` with a content-defined height and `#content` taking the remaining space in between.

`#content` already was `position: relative` for other reasons, **so adding `position: absolute` to the `<video>`** was enough to make it fit snugly.

Now `object-fit: contain` crops the top and bottom when the viewport's height isn't enough to fit the entire video, just like it does left and right when the viewport is too narrow.


```css
    html, body {
      height: 100%;
      margin: 0;
    }

    body {
      display: flex;
      flex-direction: column;
    }

    #content {
      height: 100%;
      position: relative; /* magic sauce II */
    }

    video {
      width: 100%;
      height: 100%;
      object-fit: cover;
      position: absolute; /* magic sauce */
    }

    /* colors for demonstration */
    #header, #footer { background: green; }
    video { background: blue; }
```

```html
      <body>
        <div id="header">...</div>
        <div id="content">
          <video src="http://www.w3schools.com/html/movie.mp4"></video>
        </div>
        <div id="footer">...</div>
      <body>
    </html>
```




 </details>



<br>
<br>
 _____________________________________________________
 _____________________________________________________
<br>
<br>


# Animation

<details><summary>Click to expand..</summary>
	
## transition delay
```css
transition: background-color 1s linear 2s, color 1s;
transition: property name | duration | timing function | delay
```

<br><br>


## Performance

### CPU Usage too high

<br>

#### translateZ
- This will composite the elements into their own layers (by tricking the browser into thinking it will be doing 3D transforms) and the browser should, in most cases, take advantage of GPU acceleration, lessening the burden on the CPU. For me this cut it down by about 20% (almost half).
```css
#XMLID_640_{
  transform: translateZ(0);
  animation: comet1Translate 7.5s 3s ease-in-out alternate;
}
```

<br><br>

#### keyframes
- The more keyframes you have in the animation, the more taxing it will be as well. Just try the animation with the middle or other keyframe cut out and you will see another substantial (~10-12%) drop in CPU usage.(Short: So only use 0% and 100% if you can)
```css
@keyframes starsopacity {
  0% {
    filter: blur(0em);
    opacity:1;
  }
  
  100% {
    filter: blur(1px);
    opacity: .25;
  }
}

#XMLID_660_{
  transform: translateZ(0);
  animation: starsopacity 2.5s 1s ease-in-out infinite alternate
}
```

<br><br>

#### box-shadow
- Lastly, not all properties are equal -- box-shadow is much harder for the browser to animate smoothly than, say, background-color. Leaving all of the keyframes intact but dropping the box-shadow property, using the translateZ(0) trick had my CPU usage hovered at only 10-11%.

<br><br>

#### convert animation to .gif
- As much as it pains me to say this, for infinite-loop animations an animated .gif is going to perform much, much better than CSS3 in the current state of browser animation, especially if you plan for many of them to remain rendered on the page for some time.



<br><br>

#### will-change
- will-change property allows you to inform the browser ahead of time of what kinds of changes you are likely to make to an element, so that it can set up the appropriate optimizations before they're needed.
  - will-change: transform, opacity;



<br><br>

#### Animate endless loops with JS instead of CSS infinite to increase CPU perfomance

##### Method 1 - Change animation to ''
```ccs
@keyframes comet4Translate {
  0% {
    transform: translateX(0%) translateY(-50%);
  }

  100% {
    transform: translateX(100%) translateY(100%);
  }
}

@keyframes comet1Opacity {
  0% {
    opacity:1;
  }

  100% {
    opacity:0;
  }
}

#XMLID_640_{
  transform: scale(.8) translateX(-20%) translateY(-20%) translateZ(0);
  animation: comet4Translate 7.5s 3s ease-in-out alternate, comet1Opacity 8s .5s ease-in-out alternate;
  will-change: transform;
  will-change: opacity; 
}
```

```javascript
createAnimation = (selector, intervalDelay) => {
    setInterval(() => {
	$(selector).css('animation', 'none')

	setTimeout(() => {
	    $(selector).css('animation', '')
	}, 3000)
    }, intervalDelay)
}

// first comet
createAnimation('#XMLID_640_', 16000)
```

<br><br>

##### Method 2 - Use transition instead of animation
```ccs
#XMLID_640_{
  transform: scale(.8) translateX(-20%) translateY(-20%) translateZ(0);
  animation: comet4Translate 7.5s 3s ease-in-out alternate, comet1Opacity 8s .5s ease-in-out infinite alternate;
  will-change: transform;
  will-change: opacity; 
  opacity: 1;
}

#XMLID_640_.animated {
  transform: scale(.8) translateX(150%) translateY(150%) translateZ(0);
  opacity:0;
}
```
```javascript
let switcher
const animateViaJs = selector => {
	setInterval(() => {
	    if (!switcher) {
		switcher = true
		$(selector).css('transition', 'opacity 3s ease-in-out, transform 4s ease-in-out')
	    } else {
		switcher = false
		$(selector).css('transition', 'none')
	    }

	    document.querySelector(selector).classList.toggle('animated')
	}, 5000)
}

animateViaJs('#XMLID_640_')
```

<br><br>


<br><br>

##### Method 3 - AnimeJs
```ccs
#XMLID_640_{
  will-change: transform;
  will-change: opacity; 
  translateZ: 0;
}
```
```javascript
const createAnimeJsLoop = (selector, intervalTimer, cfg) => {
	const tl = anime({ loop:true, targets: selector, easing: 'easeInQuad', ...cfg })

	setInterval(() => {
	    tl.pause()
	    setTimeout(() => tl.restart(), 5000)
	}, intervalTimer)
}

createAnimeJsLoop('#XMLID_640_', 30000, {
opacity: [
    { value: 1, duration: 0 },
    { value: 0, duration: 2000 }
],
translateX: [
    { value: '-20%', duration: 0 },
    { value: '150%', duration: 3000 }
],
translateY: [
    { value: '-20%', duration: 0  },
    { value: '150%', duration: 3000 }
],
translateZ: 0
delay: 3000
})
```

<br><br>

##### Method 4
```ccs
.nice-block {
	 background-color: red;
	 transform: translateZ(0);
	 -webkit-transform: translateZ(0);
	 -ms-transform: translateZ(0);
	 will-change: transform;
	 transition: background-color 5s ease;
}
 .nice-block.animated {
	 background-color: white;
}
```
```javascript
var bgAnimateTimer;
function animateBg () {
  clearTimeout(bgAnimateTimer);
  bgAnimateTimer = setTimeout(function () {
    clearTimeout(bgAnimateTimer);
    bgAnimateTimer = setTimeout(function () {

      document.querySelector('.nice-block').classList.toggle('animated');

      //jQuery alternative is:
      // $('.nice-block').toggleClass('animated');

      animateBg ();
    }, 5000); //5 seconds for the animation effect
  }, 2500); //2.5 seconds between each animation
}

animateBg ();
```






</details>




































<br>
<br>

 _____________________________________________________
 _____________________________________________________

<br>
<br>


# Modify text

<details><summary>Click to expand..</summary>

## Force Line Break after space
```css
/* Method #1 */
word-spacing: 100vw;
}
```  


## Character limit
```css
/* method 1 max lines */
.text {
   overflow: hidden;
   text-overflow: ellipsis;
   display: -webkit-box;
   -webkit-line-clamp: 2; /* number of lines to show */
   -webkit-box-orient: vertical;
}

/* method 2 */
 white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  max-height: 1vmax; // use width or height
```  



```javascript
// method 3
$( "blockquote" ).each(function() {

   let trimmedString = $(this).html().match( /^[\S\s]{1,200}([a-z0-9] |$)/gmi );
   $(this).html( trimmedString[0] + '...' );

});
```

</details>





















<br>
<br>


 _____________________________________________________
 _____________________________________________________


<br>
<br>

# Responsive Tutorials
- https://1linelayouts.glitch.me/




























<br>
<br>

 _____________________________________________________
 _____________________________________________________

<br>
<br>


# Position Snippets

<details><summary>Click to expand..</summary>



<br><br>


# Center

<details><summary>Click to expand..</summary>



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
/*Using flex*/
<div style="display: flex; justify-content: center; align-items: center; gap: 10px;">
  <a href="https://www.linkedin.com/in/dennis-dd">
    <img width="30" src="https://upload.wikimedia.org/wikipedia/commons/e/e9/Linkedin_icon.svg" alt="LinkedIn"/>
  </a>
  <a href="https://www.xing.com/profile/Dennis_Demand05690">
    <img width="30" src="https://upload.wikimedia.org/wikipedia/fr/d/d2/Xing_logo.png" alt="Xing"/>
  </a>
</div>


/* Method #1 */
display: block;
margin-left: auto;
margin-right: auto;

/* Method #2 */
position: fixed; /* or absolute*/
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

</details>






























<br>
<br>


 _____________________________________________________
 _____________________________________________________


<br>
<br>

# height/width

<details><summary>Click to expand..</summary>

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
  background: url(images/bg.jpg) no-repeat center center fixed; 
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;

/* Method #2 */
  background-image: url("http://i.stack.imgur.com/2OrtT.jpg");
  background-size: cover;
  background-repeat: no-repeat;
  background-position: 50% 50%;
```  


# Auto scale SVG to parent
```css

 
/* Method #1 */

<div class="wrap">
  <svg viewBox="0 0 595.5 383.75" preserveAspectRatio="xMinYMin slice">
  </svg>
</div>

.wrap svg {
  width:  100%;
  height: 100%;
  position: absolute;
}

.wrap {
    height: 100%;
    display: grid;
}









/* Method #2*/
 <svg width="100%"
 height="100%"
 viewBox="113 128 972 600"
 preserveAspectRatio="xMidYMid meet"></svg>

```  


</details>












<br>
<br>
 _____________________________________________________
 _____________________________________________________
<br>
<br>


# align

<details><summary>Click to expand..</summary>


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

/* method 2 ul & li - You may have to give ul and li 100% height */
<ul class="memberlist">
    <li>
        <div class="memberImage"><img src="foo.jpg" /></div>
        <div class="memberInfo">John Doe</div>
    </li>
    <li>
        <div class="memberImage"><img src="foo.jpg" /></div>
        <div class="memberInfo">John Doe</div>
    </li>
    <li>
        <div class="memberImage"><img src="foo.jpg" /></div>
        <div class="memberInfo">John Doe</div>
    </li>
</ul>
```  
</details>












</details>
























<br>
<br>


 _____________________________________________________
 _____________________________________________________


<br>
<br>


# Box Shadow

<details><summary>Click to expand..</summary>

<br><br>

## Top & Bottom
```css
/* Method #1 */
  box-shadow: 
        inset 0px 11px 8px -10px #CCC,
        inset 0px -11px 8px -10px #CCC; 
```  

<br><br>

## Bottom
```css
/* Method #1 */
box-shadow: 0 8px 6px -6px #00000052;
```  


<br><br>

## Left & Right
```css
/* Method #1 */
box-shadow: 0 9px 0px 0px #ffffff00,
0 -9px 0px 0px #ffffff00,
0px 10px 15px -6px #00000042,
0px 10px 15px -6px #00000042;
```  


<br><br>

## Material Design (https://codepen.io/sdthornton/pen/wBZdXq)
```css
box-shadow: 0 19px 38px rgba(0,0,0,0.30), 0 15px 12px rgba(0,0,0,0.22);
```  
    
   
<br><br>

## Multiple layer 3D 
```css
box-shadow: 0em 0em 0em 0.2em rgb(22 237 232 / 38%),
0.5em 0.4em 0em 0.2em rgb(9 253 224 / 17%),
1.3em 1.2em 0em 0em rgb(9 253 224 / 11%),
1.8em 1.8em 0em 0em rgb(9 253 224 / 7%),
0.2em 0.2em 0.1em 0.2em rgb(12 12 12 / 0%); 

/*smaller*/
box-shadow: 0em 0em 0em 0.2em rgb(22 237 232 / 38%),
.25em .25em 0em 0.2em rgb(9 253 224 / 10%),
.5em .5em 0em 0em rgb(9 253 224 / 4%),
.75em .75em 0em 0em rgb(9 253 224 / 6%);

/* nice for big modal boxed - more layers */
box-shadow: 0em 0em 0em 0.2em rgb(22 237 232 / 38%),
0.5em 0.5em 0em 0.2em rgb(9 253 224 / 12%),
1.25em 1.25em 0em 0em rgb(9 253 224 / 11%),
1.75em 1.75em 0em 0em rgb(9 253 224 / 6%),
2.25em 2.25em 0em 0em rgb(9 253 224 / 3%),
2.75em 2.75em 0em 0em rgb(9 253 224 / 1%);
```   





<br><br>

# Animated gradient v1 **HOT**
```
/* Pulsierende Border Animation - Light Mode */
@keyframes shadowPulse {
  0% {
    box-shadow: 0 0 0 0 rgba(0, 0, 0, 0.1),
                0 0 0 10px rgba(0, 0, 0, 0.1),
                0 0 0 20px rgba(0, 0, 0, 0.05),
                0 0 30px rgba(0, 0, 0, 0.05);
  }
  50% {
    box-shadow: 0 0 0 10px rgba(0, 0, 0, 0.1),
                0 0 0 20px rgba(0, 0, 0, 0.1),
                0 0 0 30px rgba(0, 0, 0, 0.05),
                0 0 40px rgba(0, 0, 0, 0.05);
  }
  100% {
    box-shadow: 0 0 0 0 rgba(0, 0, 0, 0.1),
                0 0 0 10px rgba(0, 0, 0, 0.1),
                0 0 0 20px rgba(0, 0, 0, 0.05),
                0 0 30px rgba(0, 0, 0, 0.05);
  }
}

/* Pulsierende Border Animation - Dark Mode mit Neon Effekt */
@keyframes shadowPulseDark {
  0% {
    box-shadow: 0 0 0 0 rgba(236, 72, 153, 0.2),
                0 0 0 10px rgba(236, 72, 153, 0.15),
                0 0 0 20px rgba(147, 51, 234, 0.1),
                0 0 30px rgba(236, 72, 153, 0.1);
  }
  50% {
    box-shadow: 0 0 0 10px rgba(236, 72, 153, 0.2),
                0 0 0 20px rgba(236, 72, 153, 0.15),
                0 0 0 30px rgba(147, 51, 234, 0.1),
                0 0 40px rgba(236, 72, 153, 0.1);
  }
  100% {
    box-shadow: 0 0 0 0 rgba(236, 72, 153, 0.2),
                0 0 0 10px rgba(236, 72, 153, 0.15),
                0 0 0 20px rgba(147, 51, 234, 0.1),
                0 0 30px rgba(236, 72, 153, 0.1);
  }
}

/* Basis-Klasse für den Effekt */
.ai-card-shadow {
  box-shadow: 0 0 0 0 rgba(0, 0, 0, 0.1),
              0 0 0 10px rgba(0, 0, 0, 0.1),
              0 0 0 20px rgba(0, 0, 0, 0.05),
              0 0 30px rgba(0, 0, 0, 0.05);
  transition: all 0.6s cubic-bezier(0.4, 0, 0.2, 1);
  transform: translateY(0) scale(1);
  animation: shadowPulse 3s ease-in-out infinite;
  position: relative;
  z-index: 1;
}

/* Hover-Effekt */
.ai-card-shadow:hover {
  transform: translateY(-12px) scale(1.02);
  box-shadow: 0 0 0 10px rgba(0, 0, 0, 0.15),
              0 0 0 20px rgba(0, 0, 0, 0.1),
              0 0 0 30px rgba(0, 0, 0, 0.05),
              0 0 40px rgba(0, 0, 0, 0.05);
}

/* Dark Mode Styles */
:is(.dark) .ai-card-shadow {
  box-shadow: 0 0 0 0 rgba(236, 72, 153, 0.2),
              0 0 0 10px rgba(236, 72, 153, 0.15),
              0 0 0 20px rgba(147, 51, 234, 0.1),
              0 0 30px rgba(236, 72, 153, 0.1);
  animation: shadowPulseDark 3s ease-in-out infinite;
}

/* Dark Mode Hover */
:is(.dark) .ai-card-shadow:hover {
  transform: translateY(-12px) scale(1.02);
  box-shadow: 0 0 0 10px rgba(236, 72, 153, 0.25),
              0 0 0 20px rgba(236, 72, 153, 0.2),
              0 0 0 30px rgba(147, 51, 234, 0.15),
              0 0 40px rgba(236, 72, 153, 0.15);
}
```
- Einfach die Klasse ai-card-shadow auf ein Element anwenden und fertig! Die Animation startet automatisch und reagiert auf den Dark Mode.



v2 **HOT**
```
/* Premium Glassmorphism Card with Pulsing Shadows */

/* Base Card Styles */
.base-card-shadow {
  /* Glass Effect */
  border: 1px solid rgba(0, 0, 0, 0.12);
  background: rgba(255, 255, 255, 0.08);
  backdrop-filter: blur(8px) saturate(110%);
  -webkit-backdrop-filter: blur(8px) saturate(110%);
  
  /* Base Shadows */
  box-shadow: 0 0 0 1px rgba(0, 0, 0, 0.12),
              0 0 0 4px rgba(0, 0, 0, 0.08),
              0 0 8px rgba(0, 0, 0, 0.06);
  
  transition: all 0.6s cubic-bezier(0.34, 1.56, 0.64, 1);
}

/* Dark Mode */
:is(.dark) .base-card-shadow {
  border: 1px solid rgba(236, 72, 153, 0.4);
  background: rgba(236, 72, 153, 0.06);
  backdrop-filter: blur(8px) saturate(120%);
  -webkit-backdrop-filter: blur(8px) saturate(120%);
  box-shadow: 0 0 0 1px rgba(236, 72, 153, 0.4),
              0 0 0 4px rgba(147, 51, 234, 0.3),
              0 0 8px rgba(236, 72, 153, 0.2);
}

/* Pulsing Animation - Light Mode */
@keyframes shadowPulseInner {
  /* Base State */
  0%, 45%, 100% {
    box-shadow: 0 0 0 1px rgba(0, 0, 0, 0.12),
                0 0 0 4px rgba(0, 0, 0, 0.08),
                0 0 8px rgba(0, 0, 0, 0.06);
  }
  
  /* Build Up */
  46.5% {
    box-shadow: 0 0 0 1px rgba(0, 0, 0, 0.12),
                0 0 0 6px rgba(0, 0, 0, 0.08),
                0 0 10px rgba(0, 0, 0, 0.06);
  }
  48% {
    box-shadow: 0 0 0 1px rgba(0, 0, 0, 0.12),
                0 0 0 8px rgba(0, 0, 0, 0.08),
                0 0 12px rgba(0, 0, 0, 0.06);
  }
  49.5% {
    box-shadow: 0 0 0 1px rgba(0, 0, 0, 0.12),
                0 0 0 10px rgba(0, 0, 0, 0.08),
                0 0 15px rgba(0, 0, 0, 0.06);
  }
  
  /* Peak with Hold */
  51%, 52% {
    box-shadow: 0 0 0 1px rgba(0, 0, 0, 0.02),
                0 0 0 36px rgba(0, 0, 0, 0.015),
                0 0 52px rgba(0, 0, 0, 0.01);
  }
  
  /* Smooth Fade Out */
  54% {
    box-shadow: 0 0 0 1px rgba(0, 0, 0, 0.015),
                0 0 0 24px rgba(0, 0, 0, 0.01),
                0 0 40px rgba(0, 0, 0, 0.008);
  }
  56% {
    box-shadow: 0 0 0 1px rgba(0, 0, 0, 0.01),
                0 0 0 16px rgba(0, 0, 0, 0.008),
                0 0 30px rgba(0, 0, 0, 0.005);
  }
  58% {
    box-shadow: 0 0 0 1px rgba(0, 0, 0, 0.008),
                0 0 0 8px rgba(0, 0, 0, 0.005),
                0 0 20px rgba(0, 0, 0, 0.003);
  }
  60% {
    box-shadow: 0 0 0 1px rgba(0, 0, 0, 0.005),
                0 0 0 4px rgba(0, 0, 0, 0.003),
                0 0 10px rgba(0, 0, 0, 0.002);
  }
}

/* Pulsing Animation - Dark Mode */
@keyframes shadowPulseInnerDark {
  0%, 45%, 100% {
    box-shadow: 0 0 0 1px rgba(236, 72, 153, 0.4),
                0 0 0 4px rgba(147, 51, 234, 0.3),
                0 0 8px rgba(236, 72, 153, 0.2);
  }
  46.5% {
    box-shadow: 0 0 0 1px rgba(236, 72, 153, 0.4),
                0 0 0 6px rgba(147, 51, 234, 0.3),
                0 0 10px rgba(236, 72, 153, 0.2);
  }
  48% {
    box-shadow: 0 0 0 1px rgba(236, 72, 153, 0.4),
                0 0 0 8px rgba(147, 51, 234, 0.3),
                0 0 12px rgba(236, 72, 153, 0.2);
  }
  49.5% {
    box-shadow: 0 0 0 1px rgba(236, 72, 153, 0.4),
                0 0 0 10px rgba(147, 51, 234, 0.3),
                0 0 15px rgba(236, 72, 153, 0.2);
  }
  51%, 52% {
    box-shadow: 0 0 0 1px rgba(236, 72, 153, 0.08),
                0 0 0 36px rgba(147, 51, 234, 0.06),
                0 0 52px rgba(236, 72, 153, 0.04);
  }
  54% {
    box-shadow: 0 0 0 1px rgba(236, 72, 153, 0.06),
                0 0 0 24px rgba(147, 51, 234, 0.04),
                0 0 40px rgba(236, 72, 153, 0.03);
  }
  56% {
    box-shadow: 0 0 0 1px rgba(236, 72, 153, 0.04),
                0 0 0 16px rgba(147, 51, 234, 0.03),
                0 0 30px rgba(236, 72, 153, 0.02);
  }
  58% {
    box-shadow: 0 0 0 1px rgba(236, 72, 153, 0.03),
                0 0 0 8px rgba(147, 51, 234, 0.02),
                0 0 20px rgba(236, 72, 153, 0.01);
  }
  60% {
    box-shadow: 0 0 0 1px rgba(236, 72, 153, 0.02),
                0 0 0 4px rgba(147, 51, 234, 0.01),
                0 0 10px rgba(236, 72, 153, 0.005);
  }
}

/* Apply Animation */
.element {
  animation: shadowPulseInner 6s infinite;
}

/* Dark Mode Animation */
:is(.dark) .element {
  animation: shadowPulseInnerDark 6s infinite;
}

/* Glass Reflection Effect */
.base-card-shadow::before {
  content: '';
  position: absolute;
  inset: 0;
  border-radius: inherit;
  padding: 1px;
  background: linear-gradient(
    135deg,
    rgba(255, 255, 255, 0.25) 0%,
    rgba(255, 255, 255, 0.1) 50%,
    transparent 100%
  );
  -webkit-mask: linear-gradient(#000 0 0) content-box,
                linear-gradient(#000 0 0);
  -webkit-mask-composite: xor;
  mask-composite: exclude;
  pointer-events: none;
}

/* Dark Mode Reflection */
:is(.dark) .base-card-shadow::before {
  background: linear-gradient(
    135deg,
    rgba(236, 72, 153, 0.2) 0%,
    rgba(147, 51, 234, 0.15) 50%,
    transparent 100%
  );
}

/* Hover Effects */
.base-card-shadow:hover {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px) saturate(120%);
  -webkit-backdrop-filter: blur(10px) saturate(120%);
}

:is(.dark) .base-card-shadow:hover {
  background: rgba(236, 72, 153, 0.08);
  backdrop-filter: blur(10px) saturate(130%);
  -webkit-backdrop-filter: blur(10px) saturate(130%);
}
```


    
   
    
</details>
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    


























    
    
    

<br>
<br>


 _____________________________________________________
 _____________________________________________________


<br>
<br>

# Transition

## Add delay to specific property
```css
transition: height 0.35s ease, 
            width 0.35s ease, 
            margin 0.35s ease, 
            border-color 0.35s 0.35s ease; /* notice how the delay is added here alone */
```



<br>
<br>























 _____________________________________________________
 _____________________________________________________


<br>
<br>

# textarea

## Hide all borders/resize/glow/..
```css
textarea {
    border: none;
    overflow: auto;
    outline: none;

    -webkit-box-shadow: none;
    -moz-box-shadow: none;
    box-shadow: none;

    resize: none; /*remove the resize handle on the bottom right*/
}
```




































<br>
<br>


 _____________________________________________________
 _____________________________________________________


<br>
<br>


# Z-index not working
```css
/* Method #1 (disable pointer events of the layer which is blocking the element which needs to be clicked) */
    pointer-events: none;
```  








































<br>
<br>


 _____________________________________________________
 _____________________________________________________


<br>
<br>


# Scrollbar Definition
![alt tag](https://i.stack.imgur.com/V1ElK.png)



<br>
<br>


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



        $('html').toggleClass('noscroll').css('top', '-' + $('layerone').offset().top + 'px');

        // do something..


        $('html').removeClass('noscroll');

        let root = document.querySelector(':root');
        root.setAttribute("style", "scroll-behavior: auto;");

          window.scrollTo({
              top: $('layertwo').offset().top,
              left: 0
            });

        root.setAttribute("style", "scroll-behavior: smooth;");


```































<br>
<br>

 _____________________________________________________
 _____________________________________________________


<br>
<br>

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









































<br>
<br>

 _____________________________________________________
 _____________________________________________________


<br>
<br>




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



































<br>
<br>

 _____________________________________________________
 _____________________________________________________


<br>
<br>

# Nice Fonts Collection

- https://github.com/AllThingsSmitty/fonts (maybe license..)
- https://dsgnmag.com/helvetica-alternatives-on-google-fonts/

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
font-family: 'Work Sans', sans-serif;
```


    

## Headline 



```css
/*https://fonts.google.com/specimen/Poppins?preview.text=DENNIS&preview.text_type=custom&sidebar.open=true&selection.family=Poppins:wght@900
font-family: 'Poppins', sans-serif;
*/
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@900&display=swap');



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









































<br>
<br>


 _____________________________________________________
 _____________________________________________________


<br>
<br>




<br>
<br>

# Cross Browser/Cross Devices

<details><summary>Click to expand..</summary>


## Chrome Inspector Custom Devices 
As example on windows you can find this file:
- AppData\Local\Chromium\User Data\Your profile here

Linux:
- ~/.config/google-chrome\Your profile here

Inside of Preference.json you search for this path:
- devtools.preferences.customEmulatedDeviceList

Then you can add this here for custom devices:
```javascript
"customEmulatedDeviceList":"[{\"title\":\"Desktop - FHD - 1920x1080\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1920,\"height\":1080},\"horizontal\":{\"width\":1080,\"height\":1920}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Always\"},{\"title\":\"Desktop 2700x900\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":2700,\"height\":900},\"horizontal\":{\"width\":900,\"height\":2700}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"desktop -  4k - 3840x2160\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":3840,\"height\":2160},\"horizontal\":{\"width\":2160,\"height\":3840}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Always\"},{\"title\":\"desktop - 4k other - 3440x1440\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":3440,\"height\":1440},\"horizontal\":{\"width\":1440,\"height\":3440}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Always\"},{\"title\":\"desktop - QHD - 2560x1440\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":2560,\"height\":1440},\"horizontal\":{\"width\":1440,\"height\":2560}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Always\"},{\"title\":\"desktop - 4k other v2 - 2560x1080\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":2560,\"height\":1080},\"horizontal\":{\"width\":1080,\"height\":2560}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"desktop - WUXGA - 1920x1200\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1920,\"height\":1200},\"horizontal\":{\"width\":1200,\"height\":1920}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"desktop -   WSXGA+   - 1680x1050\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1680,\"height\":1050},\"horizontal\":{\"width\":1050,\"height\":1680}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"desktop -   HD+   - 1600x900\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1600,\"height\":900},\"horizontal\":{\"width\":900,\"height\":1600}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Always\"},{\"title\":\"desktop - hd other v1 - 1536x864\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1536,\"height\":864},\"horizontal\":{\"width\":864,\"height\":1536}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Always\"},{\"title\":\"desktop -    WXGA+   - 1440x900\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1449,\"height\":900},\"horizontal\":{\"width\":900,\"height\":1449}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"desktop - hd default v1 - 1366x768\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1366,\"height\":768},\"horizontal\":{\"width\":768,\"height\":1366}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"desktop - hd default v2 smaller - 1360x768\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1360,\"height\":768},\"horizontal\":{\"width\":768,\"height\":1360}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"desktop - SXGA - 1280x1024\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1280,\"height\":1024},\"horizontal\":{\"width\":1024,\"height\":1280}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"desktop - WXGA v3 - 1280x800\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1280,\"height\":800},\"horizontal\":{\"width\":800,\"height\":1280}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"desktop - WXGA v2 - 1280x768\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1280,\"height\":768},\"horizontal\":{\"width\":768,\"height\":1280}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"desktop - WXGA v1 - 1280x720\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1280,\"height\":720},\"horizontal\":{\"width\":720,\"height\":1280}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Always\"},{\"title\":\"desktop -    XGA+    - 1152x864\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1152,\"height\":864},\"horizontal\":{\"width\":864,\"height\":1152}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"desktop - XGA - 1024x768\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1024,\"height\":768},\"horizontal\":{\"width\":768,\"height\":1024}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"desktop - WSVGA - 1024x600\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1024,\"height\":600},\"horizontal\":{\"width\":600,\"height\":1024}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Always\"},{\"title\":\"desktop - SVGA - 800x600\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":800,\"height\":600},\"horizontal\":{\"width\":600,\"height\":800}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"tablet - ipad/ipad mini - 768x1024\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (iPad; CPU OS 6_0 like Mac OS X) AppleWebKit/536.26 (KHTML, like Gecko) Version/6.0 Mobile/10A406 Safari/8536.25\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":768,\"height\":1024},\"horizontal\":{\"width\":1024,\"height\":768}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Always\"},{\"title\":\"tablet - ipad pro - 1024x1366\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (iPad; CPU OS 11_3 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/11.0 Mobile/15E148 Safari/604.1\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1024,\"height\":1366},\"horizontal\":{\"width\":1366,\"height\":1024}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"tablet - nexus 7(2013) - 600x960\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (Linux; Android 4.4; Nexus 7 Build/KRT16M) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/30.0.1599.92 Safari/537.36\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":600,\"height\":960},\"horizontal\":{\"width\":960,\"height\":600}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"tablet-GalaxyTab 10/kindle hdx/nexus10 - 800x1280\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (Linux; Android 4.4.2; Nexus 10) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.110 Safari/537.36\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":800,\"height\":1280},\"horizontal\":{\"width\":1280,\"height\":800}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"tablet - Chromebook Pixel - 1280x850\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (Linux; Android 9; Mediatek MT8173 Chromebook Build/R80-12739.94.0; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/80.0.3987.132 Safari/537.36MoodleMobile escoffier\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1280,\"height\":850},\"horizontal\":{\"width\":850,\"height\":1280}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"handy - iPhone XS Max/XR - 414 x 896\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (iPhone; CPU iPhone OS 13_3_1 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Mobile/15E148 [FBAN/FBIOS;FBDV/iPhone11,6;FBMD/iPhone;FBSN/iOS;FBSV/13.3.1;FBSS/3;FBID/phone;FBLC/en_US;FBOP/5;FBCR/]\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":414,\"height\":896},\"horizontal\":{\"width\":896,\"height\":414}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"handy - iPhone X/XS - 375 x 812\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (iPhone; CPU iPhone OS 13_3_1 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Mobile/15E148 [FBAN/FBIOS;FBDV/iPhone11,2;FBMD/iPhone;FBSN/iOS;FBSV/13.3.1;FBSS/3;FBID/phone;FBLC/en_US;FBOP/5;FBCR/]\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":375,\"height\":812},\"horizontal\":{\"width\":812,\"height\":375}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Always\"},{\"title\":\"handy - iPhone 6/7/8 - 375 x 667\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (iPhone; CPU iPhone OS 12_4_5 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Mobile/15E148 [FBAN/FBIOS;FBDV/iPhone7,2;FBMD/iPhone;FBSN/iOS;FBSV/12.4.5;FBSS/2;FBID/phone;FBLC/en_US;FBOP/5;FBCR/]\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":375,\"height\":667},\"horizontal\":{\"width\":667,\"height\":375}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"handy - iPhone 6/7/8 Plus - 414 x 736\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (iPhone; CPU iPhone OS 12_4_5 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Mobile/15E148 [FBAN/FBIOS;FBDV/iPhone7,1;FBMD/iPhone;FBSN/iOS;FBSV/12.4.5;FBSS/3;FBID/phone;FBLC/en_US;FBOP/5;FBCR/]\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":414,\"height\":736},\"horizontal\":{\"width\":736,\"height\":414}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"handy - iPhone 5 - 320 x 568\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (iPhone; CPU iPhone OS 5_0 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9A334 Safari/7534.48.3\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":320,\"height\":568},\"horizontal\":{\"width\":568,\"height\":320}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Always\"},{\"title\":\"handy - Nexus 6+6P+5X/ pixel 2 - 412 x 732\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (Linux; Android 7.0; Nexus 6 Build/NBD92G) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.83 Mobile Safari/537.36\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":412,\"height\":732},\"horizontal\":{\"width\":732,\"height\":412}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"handy - Google Pixel 3 XL - 412 x 847\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (Linux; Android 10; Pixel 3 XL) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.93 Mobile Safari/537.36\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":412,\"height\":847},\"horizontal\":{\"width\":847,\"height\":412}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"handy - Google Pixel 2 XL - 412 x 824\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (Linux; Android 10; Pixel 2 XL) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.93 Mobile Safari/537.36\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":412,\"height\":824},\"horizontal\":{\"width\":824,\"height\":412}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"handy - Samsung Galaxy Note 5/nokia 9 - 480 x 853\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (Linux; Android 6.0.1; RedMi Note 5 Build/RB3N5C; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/68.0.3440.91 Mobile Safari/537.36\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":480,\"height\":853},\"horizontal\":{\"width\":853,\"height\":480}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"handy - Samsung Galaxy S9 & Note 9 - 360 x 740\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (Linux; Android 10; Redmi Note 9S) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.106 Mobile Safari/537.36\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":360,\"height\":740},\"horizontal\":{\"width\":740,\"height\":360}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"handy-bbz30/lumia550+950/note 2+3/S3+5+7/nexus5\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (Linux; U; Android 5.0.2; en-us; Redmi Note 2 Build/LRX22G) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/42.0.0.0 Mobile Safari/537.36 XiaoMi/MiuiBrowser/2.1.1\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":360,\"height\":640},\"horizontal\":{\"width\":640,\"height\":360}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"desktop - 8K LCD TV - 7680×4320\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":7680,\"height\":4320},\"horizontal\":{\"width\":4320,\"height\":7680}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"desktop - 8k v2 - 7680-2160\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":7680,\"height\":2160},\"horizontal\":{\"width\":2160,\"height\":7680}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"handy - iPhone 4 - 320x480\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (iPhone; CPU iPhone OS 7_1_2 like Mac OS X) AppleWebKit/537.51.2 (KHTML, like Gecko) Mobile/11D257 [FBAN/FBIOS;FBAV/62.0.0.43.141;FBBV/36454510;FBRV/0;FBDV/iPhone3,2;FBMD/iPhone;FBSN/iPhone OS;FBSV/7.1.2;FBSS/2;FBCR/Orange;FBID/phone;FBLC/pl_PL;FBOP/5]\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":320,\"height\":480},\"horizontal\":{\"width\":480,\"height\":320}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"deskop - laptop touch - 1280x950\",\"type\":\"unknown\",\"user-agent\":\"\",\"capabilities\":[\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":1280,\"height\":950},\"horizontal\":{\"width\":950,\"height\":1280}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"tablet - blackberry playbook - 600x1024\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (PlayBook; U; RIM Tablet OS 1.0.0; en-US) AppleWebKit/534.8+ (KHTML, like Gecko) Version/0.0.1 Safari/534.8+\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":600,\"height\":1024},\"horizontal\":{\"width\":1024,\"height\":600}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"handy - lg optimus l70/nexus 4 - 384-640\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (Linux; Android 4.4.2; Nexus 4 Build/KOT49H) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/34.0.1847.114 Mobile Safari/537.36\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":384,\"height\":640},\"horizontal\":{\"width\":640,\"height\":384}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"},{\"title\":\"handy - nokia lumia 520 - 320x533\",\"type\":\"unknown\",\"user-agent\":\"Mozilla/5.0 (Mobile; Windows Phone 8.1; Android 4.0; ARM; Trident/7.0; Touch; rv:11.0; IEMobile/11.0; NOKIA; Lumia 520) like iPhone OS 7_0_3 Mac OS X AppleWebKit/537 (KHTML, like Gecko) Mobile Safari/537\",\"capabilities\":[\"mobile\",\"touch\"],\"screen\":{\"device-pixel-ratio\":0,\"vertical\":{\"width\":320,\"height\":533},\"horizontal\":{\"width\":533,\"height\":320}},\"modes\":[{\"title\":\"\",\"orientation\":\"vertical\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}},{\"title\":\"\",\"orientation\":\"horizontal\",\"insets\":{\"left\":0,\"top\":0,\"right\":0,\"bottom\":0}}],\"show-by-default\":true,\"show\":\"Default\"}]"

```

More viewports can be found here:
- https://viewportsizes.com/

<br>
<br>


## Cross Browser Support
- http://caniuse.com

## Cross Browser Testing - VIEWPORT
- https://bluetree.ai/screenfly/?u=https%3A//bing.com&a=20&b=10 ★ **FREE - ONLINE** ★
- http://www.responsinator.com/?url=bing.com ★ **FREE - ONLINE - Only iphone as it seems** ★
- http://browsershots.org/http://www.bing.com/ ★ **FREE - ONLINE - Only screenshots of desktop browser** ★

## Cross Browser Testing - EMULATED DEVICES
- https://www.browserstack.com/ ★ **PREMIUM - ONLINE** ★
- https://developer.android.com/studio ★ **FREE - OFFLINE** ★
- https://visualstudio.microsoft.com/vs/msft-android-emulator/  ★ **FREE - OFFLINE** ★

## Responsive Scale
- https://codepen.io/cRckls/pen/mcGCL


## Remote Debugging on own smartphones
- https://developers.google.com/web/tools/chrome-devtools/remote-debugging


<br>
<br>

## Use Inspector on smartphones

### IOS (https://github.com/liriliri/eruda)
Create bookmark and replace site link with this code (https://www.youtube.com/watch?v=fTh9ESsWklM):
```javascript
javascript:(function () { var script = document.createElement('script'); script.src="//cdn.jsdelivr.net/npm/eruda"; document.body.appendChild(script); script.onload = function () { eruda.init() } })();
```

<br>
<br>

# Android Studio

## Cant install HXAM
- Download HAXM manually from here: https://github.com/intel/haxm/releases/tag/v7.6.1

## Show avaible devices
- C:\Users\Administrator\AppData\Local\Android\Sdk\emulator\emulator.exe -list-avds

## Start emulator from command line
```bash
C:\Users\Administrator\AppData\Local\Android\Sdk\emulator\emulator.exe -avd Pixel_3a_API_30 -dns-server 8.8.8.8 -gpu host -noaudio
```

## adb can´t connect to deamon
This fix maybe not really solve the problem but atleast adb is starting..
```bash
adb nodaemon server
adb start-server
```

## Connect to host os localhost from emulated devices
- In my cases I disabled "Use Android Studio HTTP proxy setting" on the settings area of the emulated devices (three dots on the sidebar > Settings > Proxy)
- You can visit inside of your emulated device browser 10.0.2.2 to reach localhost from your host os!

## Open emulated device browser inspector on your main os
- chrome://inspect/#devices

## Increase performance
Open config.ini (AVD Manager click arrow and then show on disk) and add:
```bash
hw.audioInput=no
hw.audioOutput=no
```

Disable Multi-Core and enable Hardware for Graphics
![alt tag](https://i.stack.imgur.com/dcheJ.png)


</details>











































<br>
<br>

 _____________________________________________________
 _____________________________________________________


<br>
<br>






# Third Party Collections


<details><summary>Click to expand..</summary>

## Material Design
- Bootstrap 4 Collection: https://codepen.io/mdbootstrap/pen/LRNZBz

## Full websites
- https://codepen.io/veronicadev/details/YYvjzO
- https://codepen.io/team/webflow/pen/pvydKd




<br>
<br>





## Email templates

#### How to send html mail via gmail:
- https://www.youtube.com/watch?v=MsMSqhMlfao

#### How to send html mail via AppScript (https://codegena.com/send-mail-merge-html-emails-using-google-appscripts/):
- The following code is all you require to send an HTML email to your friend. To run this code, head over to script.google.com and create a new one. Paste the following code into the editor. Now create the email template by clicking File > New > HTML file. Make sure that the HTML file name matches the name we provide in the code.

```javascript
function myFunction(){

  
  // html email
  var htmlEmailBody = HtmlService.createTemplateFromFile('html-template-name');

  // email title
  var subject = "sample title..";
  
  // this must be set or .sendEmail will not work. You can insert your own email address to get a copy of the email or just let it blank. Alternative you can delete bcc and just the emailAddress value to send 1 email only.
  var emailAddress = "";
  
  // same like emailAddress this must be set aswell. You can just keep it blank and use htmlBody for your html email. Alternative delete htmlBody and use normalBody for plain text email instead.
  var normalBody = "";
 
  // find any file with this name on your gdrive. If not found email will not be sended..
  var file = DriveApp.getFilesByName('resume_en.pdf');
  
  
  
  
  if (file.hasNext()) {


MailApp.sendEmail(emailAddress, subject, normalBody, {
  name: "Dennis Demand",
  attachments: [file.next().getAs(MimeType.PDF)],
  htmlBody: htmlEmailBody.evaluate().getContent(),
  bcc: 'sample1@gmail.com,sample2@web.de'
});
    
  }


    

}
```

#### Supported CSS/HTML 
https://www.caniemail.com


- Responsive multi layer: https://codepen.io/rodriguezcommaj/pen/RNPzwr ★ **HOT** - TESTED FOR EMAIL USAGE ★
- Responsive: https://codepen.io/rickygipson/pen/Aouhi
- Responsive: https://codepen.io/zavoloklom/pen/qEVqzx
- Responsive: https://github.com/konsav/email-templates/ (https://github.com/konsav/email-templates/)
- Responsive: https://codepen.io/raybeezdesign/pen/pHlLG
- Responsive multi layer: https://codepen.io/Mestika/pen/bEerrv  ★ **HOT** ★
- responsive layout: https://codepen.io/beeeees/pen/JEDms
- responsive multi layer: https://codepen.io/brucej/pen/BjdwVj  ★ **HOT** - TESTED FOR EMAIL USAGE ★
- responsive: https://codepen.io/RyanHallMedia/pen/qRXBKW
- responsive multi layer: https://codepen.io/reallygoodemails/pen/ZWqOBz
- small clean: https://codepen.io/koca/pen/vjzyad
- responsive multi layer: https://codepen.io/maizzle/pen/WYjyvg  ★ **HOT** - TESTED FOR EMAIL USAGE ★
- animated?: https://codepen.io/reallygoodemails/pen/yJagbN
- small clean: https://codepen.io/shift-tech/pen/eMdePP
- small clean: https://codepen.io/denner-rondinely/pen/qwdywa
- small clean: https://codepen.io/dvomaks/pen/xedjBp
- small clean: https://codepen.io/darcyturk/pen/XxdVbv
- material design: https://codepen.io/judecodes/pen/YBdMLZ
- small clean: https://codepen.io/mtthlbg/pen/KVWggg
- material design multi layer: https://codepen.io/luong-quynh/pen/agBMbg  ★ **HOT** - Doesnt work real emails..★
- clean card with bg: https://codepen.io/faudau/pen/zJombX
- product offer: https://codepen.io/reallygoodemails/pen/OMqpmN  ★ **HOT** ★
- small clean: https://codepen.io/MarcoZani/details/aRNQmQ
- clean: https://codepen.io/koolkamalkishor/pen/ZEbgyrj
- transition image: https://codepen.io/Romaric_aboule/pen/gOpywgG
- clean card: https://codepen.io/saurya3579/pen/poJKdWP
- clean: https://codepen.io/visionarymarketer/pen/rLqZqx
- image transition: https://codepen.io/Mr_Rahul_Tiwari/pen/Wqzqpd
- clean big image: https://codepen.io/reallygoodemails/pen/ELoOvj






## Image Gird
- https://codepen.io/dtab428/pen/bRwMeq
- https://codepen.io/JohnRiordan/details/Xbjwqe
- https://codepen.io/tstoik/pen/qZEZJp
- https://codepen.io/team/keyframers/pen/EzMyQe



<br><br>

## Text
- Shimmer effect: https://codepen.io/redouglas/pen/gobsm

<br>

### Multiple Shadows
- https://codepen.io/tommyho/pen/abejXMb





<br><br>

## Lightbox:
- https://codepen.io/ezra_siton/pen/XNpJaX
- https://photoswipe.com/
- https://nanogallery2.nanostudio.org/
- https://biati-digital.github.io/glightbox/
- https://simplelightbox.com/
- Lightgallery Plugin (commercial not free): https://codepen.io/sachinchoolur/pen/QjLNMM
- Single Image: https://codepen.io/gschier/pen/HCoqh
- Single Image: https://codepen.io/ongtiffany/pen/BoOeQV
- Gallery: https://codepen.io/nsom/pen/VbqLew
- Animated Gallery: https://codepen.io/designcouch/pen/DEkcf
- Gallery: https://codepen.io/svelts/pen/VYxPWW
- Grid Gallery with animation to center: https://codepen.io/ademilter/pen/ByLwwV

<br><br>

## Easing
- Cheat Sheet: https://easings.net/ - https://animejs.com/documentation/#pennerFunctions


<br><br>

# Music Player
- https://codepen.io/ecemgo/pen/vYPadZz

<br><br>


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
- Sticky Cursor **HOT** https://codepen.io/dev_loop/pen/abxJMxL

## Mouse Cursor SVG Collection
- https://mega.nz/file/y3pUUCZS#NPEm6f00U2VLweB0BXLL5yf5BUU53Ndd4f0b-TvW534

## Spinner
- loading.io <-- great site
- https://codepen.io/ahmadbassamemran/pen/bXRPdr
- https://codepen.io/akhil_001/pen/YqBZgL
- https://tobiasahlin.com/spinkit/
- Windows 10: https://codepen.io/jenning/pen/rrkBbq
- https://codepen.io/Godwin/pen/eWBzNX
- Big Circle 3d effect: https://codepen.io/mattbhenley/pen/gQgVxG
- Loader: https://codepen.io/PicturElements/pen/ZOwkwv
- Atom Loader: https://codepen.io/dmsanchez86/details/WxRovR
- Google Loader: https://codepen.io/AmineMohamed/pen/JZxyYm
- https://codepen.io/grssam/details/nZyxQN **HOT**

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
- Pulsing animated (https://codepen.io/emileaublet/pen/PNvNma) **HOT**
- call button (https://codepen.io/get-web/pen/bGdVOWq) **HOT**
- general button (https://codepen.io/simeydotme/pen/ZEgJoXB) **HOT**
- https://ryanmulligan.dev/blog/pixel-canvas/ **hot**
  -  https://github.com/hexagoncircle/pixel-canvas 

## Dark/white Mode Button
- https://codepen.io/jh3y/pen/ByBjxrW **HOT**


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








## Chat UI
- https://codepen.io/Momciloo/pen/bEdbxY



## Pagination
- https://codepen.io/hakimel/details/gfIsk
- https://codepen.io/netzzwerg/pen/hfutI
- Infinity (https://codepen.io/MarioD/pen/OmWaqz)
- svg animated (https://codepen.io/chrisgannon/pen/xVOjZq)
- morphing patination (https://codepen.io/aaroniker/pen/pojXjrZ)



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
- hover with tooltip: https://codepen.io/kieranfivestars/pen/gbOWbM

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
- Responsive card slider (https://codepen.io/JavaScriptJunkie/pen/WgRBxw)
- Gradient **HOT** - https://codepen.io/kristen17/pen/NPKrxBd
- Gradien Border **HOT** https://codepen.io/jh3y/pen/WNmQXyE

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
- Free Vector logos with backlink:
  - https://www.freepik.com/search?format=search&page=2&query=search+engine
  - pngtree.com





<br><br>

## 3D
- card with mouse follow: https://codepen.io/lembitk/pen/EVmqmY
- https://codepen.io/yotman/pen/VEzXJp
- Image Carousel: https://codepen.io/hoanghien0410/pen/MMPaqm
- glassorphic logo (https://codepen.io/konstantindenerz/pen/VwoEJqP)
- three.js cards (https://codepen.io/smcnally000/pen/eYqXWyJ)




<br><br>


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
- Material Design small (https://codepen.io/rkpasia/pen/LNEQod) *HOT*







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
- Responsive Vertical Scrolling Parallax Gallery **HOT**  https://codepen.io/noirsociety/pen/NWJvgZg

## Image Transitions
- https://codepen.io/sfi0zy/pen/OQOExE

















## Border Animation
- https://codepen.io/Rplus/pen/lEDBj
- https://codepen.io/uiswarup/pen/RBByzW
- https://codepen.io/littlesnippets/pen/oLajBa
- Gradient Border: https://codepen.io/mike-schultz/pen/NgQvGO
- https://codepen.io/pineappleSyrup/pen/gNdERJ **HOT**
- https://codepen.io/ZachSaucier/pen/nMRbQN **HOT**
- https://codepen.io/Huhtamaki/pen/GPzwPY **HOT**



## Text animation
- https://codepen.io/team/keyframers/pen/vYNyWwQ
- https://codepen.io/KaioRocha/pen/YoEVvZ



## Popup
- https://codepen.io/melnik909/pen/QModrM





<br><br>
<br><br>

## Background
- https://loading.io/background/
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
- POV moving hills ride: https://codepen.io/ykob/pen/aBrjaR
- Infinite Falling Illusion | WebGL Shader **HOT** (https://codepen.io/pjkarlik/pen/mybEwjG)

<br><br>

### WebGL Backgrounds
- https://github.com/PavelDoGreat/WebGL-Fluid-Simulation
- https://www.vantajs.com/?effect=trunk **HOT**

<br><br>

### Canvas Backgrounds
- https://github.com/crnacura/AmbientCanvasBackgrounds?tab=readme-ov-file

<br><br>

### Background Images (cc0)
- Developer on bench: https://pixabay.com/photos/work-workaholic-writer-programmer-1627703/

<br><br>

### Animated Gradient Background
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




</details>















































<br><br>
<br><br>

 _____________________________________________________
 _____________________________________________________

<br><br>
<br><br>


## Fonts for Developer
- https://github.com/tonsky/FiraCode  ★ **HOT** ★
- Roboto
- Source Code Pro
- https://pcaro.es/p/hermit/ ★ **HOT** ★
- https://sourcefoundry.org/hack/
- https://input.fontbureau.com/download/
- https://github.com/kosimst/Firicico
- https://github.com/belluzj/fantasque-sans
- https://www.levien.com/type/myfonts/inconsolata.html
- https://typeof.net/Iosevka/
- https://damieng.com/blog/2008/05/26/envy-code-r-preview-7-coding-font-released
- https://www.dafont.com/dec-terminal-modern.font


