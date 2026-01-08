# Browser & Document Object Model

## Table of Contents


## Window Object
- [Window API Specs](https://developer.mozilla.org/en-US/docs/Web/API/Window)

### Instance Properties
- [window.document](https://developer.mozilla.org/en-US/docs/Web/API/Window/document)

#### [`window.document`](https://developer.mozilla.org/en-US/docs/Web/API/Window/document)

#### [`window.window`](https://developer.mozilla.org/en-US/docs/Web/API/Window/window)

#### [`window.location`](https://developer.mozilla.org/en-US/docs/Web/API/Window/location)

#### [`window.navigator`](https://developer.mozilla.org/en-US/docs/Web/API/Window/navigator)

#### [`window.screen`](https://developer.mozilla.org/en-US/docs/Web/API/Window/screen)

#### [`window.history`](https://developer.mozilla.org/en-US/docs/Web/API/Window/history)

#### [`window.innerWidth`](https://developer.mozilla.org/en-US/docs/Web/API/Window/innerWidth)

#### [`window.innerHeight`](https://developer.mozilla.org/en-US/docs/Web/API/Window/innerHeight)

#### [`window.outerWidth`](https://developer.mozilla.org/en-US/docs/Web/API/Window/outerWidth)

#### [`window.outerHeight`](https://developer.mozilla.org/en-US/docs/Web/API/Window/outerHeight)

#### [`window.sessionStorage`](https://developer.mozilla.org/en-US/docs/Web/API/Window/sessionStorage)

#### [`window.localStorage`](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)


### Instance Methods
#### [`window.alert()`](https://developer.mozilla.org/en-US/docs/Web/API/Window/alert)

#### [`window.confirm()`](https://developer.mozilla.org/en-US/docs/Web/API/Window/confirm)

#### [`window.prompt()`](https://developer.mozilla.org/en-US/docs/Web/API/Window/prompt)

#### [`window.getComputedStyle()`](https://developer.mozilla.org/en-US/docs/Web/API/Window/getComputedStyle)

#### [`window.postMessage()`](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)

#### [`window.focus()`](https://developer.mozilla.org/en-US/docs/Web/API/Window/focus)

#### [`window.matchMedia()`](https://developer.mozilla.org/en-US/docs/Web/API/Window/matchMedia)

#### [`window.queueMicrotask()`](https://developer.mozilla.org/en-US/docs/Web/API/Window/queueMicrotask)

## [Viewport & CSSOM](https://developer.mozilla.org/en-US/docs/Web/API/CSS_Object_Model)
- [Viewport & CSSOM API Specs](https://developer.mozilla.org/en-US/docs/Web/API/CSS_Object_Model)
- [Viewport & CSSOM Guide](https://developer.mozilla.org/en-US/docs/Web/API/CSS_Object_Model/Introduction)
- [Viewport & CSSOM Reference](https://developer.mozilla.org/en-US/docs/Web/API/CSS_Object_Model/Reference)
### [Viewport Concepts](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/CSSOM_view/Viewport_concepts)
- [Viewport Concept Guide](https://developer.mozilla.org/en-US/docs/Glossary/Viewport)
- [Understanding Viewport Units](https://developer.mozilla.org/en-US/docs/Web/CSS/Viewport_units)

#### [Visual Viewport](https://developer.mozilla.org/en-US/docs/Glossary/Visual_Viewport)
The visual viewport is the portion of a webpage that is currently visible to the user.
#### [Layout Viewport](https://developer.mozilla.org/en-US/docs/Glossary/Layout_Viewport)
The layout viewport is the area used by the browser to lay out the webpage. It may be larger than the visual viewport, especially on mobile devices where users can zoom in and out.

### [CSSOM - CSS Object Model (CSSOM) API Specs](https://developer.mozilla.org/en-US/docs/Web/API/CSSOM_view_API)
The CSSOM view API lets you manipulate the visual view of a document, including getting the position of element layout boxes, **obtaining the width or height of the viewport through script**, and also scrolling an element.
### CSSOM Concepts
- [CSS Object Model (CSSOM) Concepts](https://developer.mozilla.org/en-US/docs/Web/API/CSS_Object_Model/Concepts)
- [CSSOM Coordinate Systems](https://developer.mozilla.org/en-US/docs/Web/API/CSSOM_view_API/Coordinate_systems)
- 
### Interfaces



```js
// window.getComputedStyle(element): method returns a live read-only 
// CSSStyleProperties object containing the resolved values of all CSS 
// properties of an element, after applying active stylesheets and 
// resolving any computation those values may contain
// it uses js notation for css properties (e.g., backgroundColor instead of background-color).
// https://developer.mozilla.org/en-US/docs/Web/API/Window/getComputedStyle
// @example getComputedStyle(element)
// @or getComputedStyle(element, pseudoElt)

// CSSStyleProperties object: represents an object that is a map of CSS property names 
// to their values. It is returned by the Window.getComputedStyle() method.
// https://developer.mozilla.org/en-US/docs/Web/API/CSSStyleDeclaration
// https://developer.mozilla.org/en-US/docs/Web/API/CSSStyleProperties

// .getPropertyValue('--variable-name'): Extracts the specific value of a CSS custom property. 

// MediaList interface represents the media queries of a stylesheet, 
// e.g., those set using a <link> element's media attribute.
// https://developer.mozilla.org/en-US/docs/Web/API/MediaList
// @methods: appendMedium(), deleteMedium(), item(), toString()
// @InstanceProperties: length, mediaText



// window.postMessage() method safely enables cross-origin communication between Window objects; 
// e.g., between a page and a pop-up that it spawned, 
// or between a page and an iframe embedded within it.
// https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage

// window.prompt() instructs the browser to display a dialog with an optional 
// message prompting the user to input some text, and to wait until 
// the user either submits the text or cancels the dialog.
// https://developer.mozilla.org/en-US/docs/Web/API/Window/prompt

// queueMicrotask() method of the Window interface queues a microtask to be executed 
// at a safe time prior to control returning to the browser's event loop.
//queueMicrotask(() => {
//  function contents here...
// });
// The microtask is a short function which will run after the current task has 
// completed its work and when there is no other code waiting to be run before control 
// of the execution context is returned to the browser's event loop.
// https://developer.mozilla.org/en-US/docs/Web/API/Window/queueMicrotask
// @example 
// if (clicked) {
//   window.focus();
// }

// window.focus() method sets focus on the current window.
// https://developer.mozilla.org/en-US/docs/Web/API/Window/focus
// @example window.focus()

// MediaQueryList object stores information on a media query applied to a document, 
// with support for both immediate and event-driven matching against the state of the document.
// https://developer.mozilla.org/en-US/docs/Web/API/MediaQueryList
// @properties: media, matches
// @methods: addListener(), removeListener(), addEventListener(), removeEventListener(), dispatchEvent()

// window.matchMedia() method returns a new MediaQueryList object
// representing the results of the specified CSS media query string.
// https://developer.mozilla.org/en-US/docs/Web/API/Window/matchMedia
// @example window.matchMedia("(max-width: 600px)")
```


