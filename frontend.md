# Frontend Notes

---

1. HTML
    1. [HTML Senmantic Tags](#html-semantic-tags)
    2. [meta viewport](#meta-viewport)
    3. [Common HTML5 Tags](#common-html5-tags)
    4. [What is H5?](#what-is-h5?)
2. CSS
3. Vanilla JS

---

## 1. HTML

### HTML Senmantic Tags

A semantic element clearly describes its meaning to both the browser and the developer. For example, we use <p> tage for a paragraph, use h1 - h5 tags for headlines, article tag for an article, video tag for video. Non-semantic elements such as div, and span tags tell nothing about its content.

Some common bad practice includes using table, or purely divs for element arrangement. In the very begining, people used tables inside tables inside tables, and it was very difficult to maintain and update. Later people started using tons of divs and css. It was ok but not good enough.

### meta viewport

We usually just do:

```html
<meta
    name="viewport"
    content="width=device-width, initial-scale=1, maximum-scale=1, minimum-scale=1"
/>
```

The browswer's viewport is the are of the window in which web content can be seen. This is often not the same size as the rendered page, that's why we have scroll bars to access all the content.

The narrowscreen devices render the page in a vritual window or viewport and then shrink it down to the screen width. the width controls the size of the viewport, initial sclae controls the zoom level when the page is first loaded. maximum scale and minimum sclae controls how much the user can zoom in and out.

### Common HTML5 Tags

header, main, article, footer, aside.
canvas

1. document.getElementById >> find canvas
2. canvas.getContext >> get context, 2D graphics, WebGL does 3d
3. fillStyle adjusts the color
4. fillRect defines the rectangle

```js
const canvas = document.getElementById("canvas");
const ctx = canvas.getContext("2d");

ctx.fillStyle = "green";
ctx.fillRect(10, 10, 150, 100);
```

, video (attributes: src, autoplay, controls, poster, type, height, width), audio (attributes: src, autoplay, controls), figure

### What is H5?

HTML5 is a standard, but H5 development is a collection of technologies including:

1. Webpage preloading
2. Loading audio
3. Swiping for scrolling (use touch events)
4. Draw and earse with swiping (canvas)
5. Animated text and images (css3 animation and js)
6. Forms
7. Supports image and text uploading.

## 2. CSS

### CSS Box Model

The CSS box model is essentially a box that wraps around every HTML element. From outside to inside, it consists of: mrgins, borders,padding, and the actual content.
Setting the width and height of an element only adjusts the content box size. The full size includes padding, border, and margin.
Two types of boxes for box sizing:

-   content box: the default box inside.
-   border box: more convient, tells the browser to also account for the border, and padding.

### How to Vertically Center an Element?

If the parent does not have a defined height:
child: padding: 10px 0;

If the parent element has a height:

1. flex

```css
.parent {
    height: 100px;
    display: flex;
    justify-content: center; // primary axis alignment, default horizontal
    align-items: center; // secondary axis alignment, default vertical
}
.child {
}
```

2. Child absolute position with auto margin

```css
.parent {
    position: relative;
    /* some height */
}
.child {
    position: absolute;
    /* some height and width */
    margin: auto;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
}
```

3. Table automatically does that - not reccomended

```html
<table class="parent">
    <tr>
        <td class="child">some random text</td>
    </tr>
</table>
```

4. 100% height Inline-blocks with parent, before and after

```css
.parent {
    height: 600px;
    text-align: center;
}

.child {
    display: inline-block;
    width: 300px;
    vertical-align: middle;
}

.parent:before {
    content: "";
    display: inline-block;
    height: 100%;
    vertical-align: middle;
}
.parent:after {
    content: "";
    display: inline-block;
    height: 100%;
    vertical-align: middle;
}
```

5. Absolute position, margin-top: -50% of height pxs

```css
.parent {
    height: 600px;
    position: relative;
}
.child {
    position: absolute;
    top: 50%;
    height: 100px;
    margin-top: -50px;
}
```
