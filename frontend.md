# Frontend Notes

---

1. HTML
    1. [HTML Senmantic Tags](#html-semantic-tags)
    2. [meta viewport](#meta-viewport)
    3. [Common HTML5 Tags](#common-html5-tags)
    4. [What is H5?](#what-is-h5?)
    5. [Block vs inline Elements](#block-vs-inline-elements)
2. CSS
    1. [CSS Box Model](#css-box-model)
    2. [How to Vertically Center an Element?](#how-to-vertically-center-an-element?)
    3. [flex](#flex)
    4. [What is BFC?](#what-is-bfc?)
    5. [CSS Selector Priorities](#css-selector-priorities)
    6. [Clear Floats(Clearfix)](<#clear-floats(clearfix)>)
3. JS
    - ES6 Basics
        1. [block](#block)
        2. [let](#let)
        3. [const](#const)
        4. [Arrow functions](#arrow-functions)
        5. [Default parameters](#default-parameters)
        6. [Promise](#promise)
4. React
    1. [Functional components vs class components](#functional-components-vs-class-components)
    2. [Controlled Components vs Uncontrolled Components](#controlled-components-vs-uncontrolled-components)
    3. [React Lifecyle](#react-lifecycle)

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

### Block vs inline Elements

-   A block-level element always starts on a new line.

-   A block-level element always takes up the full width available (stretches out to the left and right as far as it can).

-   A block level element has a top and a bottom margin, whereas an inline element does not.

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

### flex

Flex container provides flex content for its direct children.
flex-flow is short for flex-direction, and flex-wrap.
justify-content values: flex-start, flex-end, center, space-between, space-around, space-evenly.

The flex property sets how a flex item will grow or shrink to fit the space available in the flex container.

flex is shorthand for flex-grow | flex-shrink | flex-basis
The second number is flex-shrink if it's a number, flex-basis if a specific value for width such as pxs, or em.

For # ##:
justify-content: space-between;
mid element: margin-left: auto;

### What is BFC?

Block formatting context(BFC)
Example: A box with "overflow: hidden" would create BFC to hide the overflown element.

It's also craeted when absolute/fixed posiiton is used.
Also with table cells, inline-blocks, direct children of the flex/grid container if they are not flex, or grid, or table containers themselves.

### CSS Selector Priorities

1. The more specifically ddefined, the higher priority:
   " :not (.xxx):first-child{}" has higher priority than just ".xxx {}". ID > class > type selectors and pseudo-elements
2. The later ones overwrites the ones above(early ones)
3. important! has highest priority, but use with caution

common wrong answer:
0000
0001
0010

### Clear Floats(Clearfix)

Elemnts after a floating element will flow around it.

```css
.clearfix {
    content: "";
    display: block / table;
    clear: both;
}
```

add this clearfix class to the container, the floats of the children elements will be cleared.

## JS

7 fundamental data types: strings, numbers, booleans, null, undefined, symbols, and object.

falsey values: 0, empty strings " ", null, undefined, NaN

### ES6 basics

#### block

(https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/block)

A block statement(compound statement) is used to group zero or more statements(basically the curly braces)

Variables declared with "var" or created by function delcarations in non-strict mode do not have block scope. They affect things beyond the block itself. Block statments do not introduce a scope.

Identifiers declared withg "let" and "const" do have block scope.

#### let

(https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)

The "let" statement declares a block-scoped local variable, optionally intitializing it to a value.

Often declare let variables at the top of the scope to avoid many issues.

##### Difference between let and var

1. Block Scope:
   let declares variables that are block scoped. var declares a variable globally or locally regardless of blcok scope.
2. Initialization:
   let is initialized to a value only when a parser evaluates it.
3. Object:
   At the top level of programs and functions, let, unlike var does not create a property on the global object.

##### Temperal dead zone (TDZ)

let variables cannot be read/writen until they have been fully initialized, which happens when they are declared.

#### const

Block-scoped, similar to let variables. Cannot be redecalred. The value of a contant can't be changed through reassignmint.

Does not mean the value it holds is immutable, just that the variable identifier cannot be reassigned. If the content is an object, the object's contents can be altered.

Convention to use all uppercase letters for const variables

Needs to be initialized.

```js
//This will throw an Uncaught SytaxERROR
const FOO;
```

#### class

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/class

The class declaration creates a new class with a given name using prototype-based inheritance.

##### Or css class

Assigns a class name or set of class names to an element. You may assign the same class name or names to any number of elements, however, multiple class names must be separated by whitespace characters.

An element's class name serves two key roles:

1. As a style sheet selector, for when an author assigns style information to a set of elements.
2. For general use by the browser.

#### arrow functions

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions

A compact/concise alternative to the tradictional function expression, but limited.

##### Difference & Limitations

-   Does not have its own bindings to "this" or "super", and should not be used as "methods"
-   Doe not have arguments, or new target keywords.
    Not suitable for "call", "apply" and "bind" methods, which generally rely on establishing a scope
-   Cannot be used as constructors
-   Cannot use "yield" within its body.

```js
// Traditional
function (a, b){
    return a + b + 100;
}

// Arrow Function
(a, b) => a + b + 100;
// if no arguments
() => a + b + 100;

// Traditional named functions
function bob (a){
    return a + 100;
}
// arrow function
let bob = a => a + 100;
```

#### Promise

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

The Promise object represents the eventual completion (or failure) of an asynchronous operation and its resulting value.

A Promise is a proxy for a value not necessarily known when the promise is created. It allows you to associate handlers with an asynchronous action's eventual success value or failure reason. This lets asynchronous methods return values like synchronous methods: instead of immediately returning the final value, the asynchronous method returns a promise to supply the value at some point in the future.

A Promise is in one of these states:

-   pending: initial state, neither fulfilled nor rejected.
-   fulfilled: meaning that the operation was completed successfully.
-   rejected: meaning that the operation failed.

#### Promise.all

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/all

The Promise.all() method takes an iterable of promises as an input, and returns a single Promise that resolves to an array of the results of the input promises. This returned promise will resolve when all of the input's promises have resolved, or if the input iterable contains no promises. It rejects immediately upon any of the input promises rejecting or non-promises throwing an error, and will reject with this first rejection message / error.

#### Promise.race

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/race

The Promise.race() method returns a promise that fulfills or rejects as soon as one of the promises in an iterable fulfills or rejects, with the value or reason from that promise.

### debounce and throttle

#### Default parameters

Default function parameters allow named parameters to be initialized with default values if no value or "undefined" is passed.

Set default value in teh function head:

```js
function (a, b = 1){
    return a * b;
}
```

#### Functional component vs class component

##### Functional(Stateless)

-   Functional components are stateless components and are easier to write. Class components hold states – stateful components.
-   Functional components are JS functions that returns html UI. It accepts props in function and return JSX(html)
-   There is no render method used in functional components.
-   These can be typically defined using arrow functions but can also be created with the regular function keyword.

##### Class(Stateful)

Class components are regular ES6 classes that extends component class from React Library. It must have render() method returning html
It has complex UI Logic
You pass props to class components and access them with this.props

#### Controlled Components vs Uncontrolled Components

```js
<MyInput value={x} onChange={fn}/> // Controlled Component
 <MyInput defaultValue={x} ref={input}/> // Uncontrolled Component
```

The state of the controlled components are handled and maintained by the developer. The uncontrolled components' states are maintained by the component itself(not controlled by the developer.

#### React Lifecyle

3 mian phases: Mounting, Updating, and Unmounting.

##### Mounting

1. constructor()
2. getDerivedStateFromProps()
3. render()
4. componentDidMount()

##### Updating

1. getDerivedStateFromProps()
2. shouldComponentUpdate()
3. render()
4. getSnapshotBeforeUpdate()
5. componentDidUpdate()

#### Unmounting

1. componentWillMount()
