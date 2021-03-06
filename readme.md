# I - JavaScript, DOM Manipulation

Today we begin introducing much of the basic JavaScript you will need for this semester - arrays, objects, template strings, functions and DOM scripting.

We also begin to cover NodeJS - focusing on Node Package Manager.

## Homework

Review the notes below. Download and unzip the files as completed by me at the end of the class [here](http://daniel.deverell.com/intermediate/session-1.zip). 'cd' into the directory and run `npm install` and then `npm run start`. (Windows users may need to edit the script in `package.json` to read `"start": "browser-sync start --server \"app\" --files \"app\""` as noted below.) Follow the instructions that begin [here](https://github.com/front-end-intermediate/session-1#exercise---faking-it), to hijack one of the hashes and emulate a single page application for the Workbook link.

If you want more information on NPM you should watch a [Node.js Tutorial for Absolute Beginners](https://youtu.be/U8XF6AFGqlc) on YouTube.

Software setup

1. Install [node.js](https://nodejs.org/en/) on your laptop
1. Install [Visual Studio Code](https://code.visualstudio.com/) on your laptop
1. Install [GIT](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) on your laptop
1. Create a Github account

## Syllabus

[Syllabus](http://daniel.deverell.com/syllabii/_intermediate-syllabus.pdf)

## The Command Line

In order to create websites you need to have a minimal set of terminal commands at your disposal.

* Note: Windows users normally use Powershell (as Administrator) but can try the Git Bash terminal that is installed along with Git when things go wrong. Some of the commands below may be different on Windows or have alternatives.

```sh
$cd
// change directory
$ cd ~
// go to your home directory
$ cd <PATH>
// Mac: copy and paste the folder you want to go to
$ cd Desk
// tab completion
$ cd ..
// go up one level
$ ls
// list files, dir on a PC
$ ls -al
// list file with flags that expand the command
$ pwd
// print working directory
```

## Node Package Manager

[Node Package Manager](https://www.npmjs.com) is an essential part of the web design and development ecosystem. [Node](https://nodejs.org/en/) includes NPM as part of its install.

## Node Package Manager (NPM) - Demo

NPM case study - A static site generator. (What is a [static site generator?](https://davidwalsh.name/introduction-static-site-generators)).

* [Wintersmith](https://github.com/jnordberg/wintersmith) - `git clone`, `npm install -g`
* [Markdown](https://en.wikipedia.org/wiki/Markdown)
* [Pug](https://www.npmjs.com/package/pug) is a [template processing language](https://en.wikipedia.org/wiki/Template_processor), it is one of [many](https://colorlib.com/wp/top-templating-engines-for-javascript/)
* [Article on pug](https://codeburst.io/getting-started-with-pug-template-engine-e49cfa291e33) (aka Jade)
* [Pug online demo](http://aramboyajyan.github.io/online-jade-template-editor/)
* [CoffeeScript](http://coffeescript.org)

## NPM Manifests

We will install and use [Browser Sync](https://www.browsersync.io) for our for foray into NPM.

`npm init` and `npm install`:

```sh
npm init // examine the new package.json
```

* `npm init` creates `package.json`

```sh
npm install browser-sync --save-dev // examine changes to the directory and package
```

* `npm install browser-sync --save-dev` installs [Browser Sync](https://www.browsersync.io) into the `node_modules` folder
* `--save-dev` adds the software to a list of development dependancies in the manifest

Summary:

* package.json
* dependencies
* node_modules folder
* the need for `.gitignore`.

### Editing package.json

* Browser Sync [Command Line (CLI) documentation](https://www.browsersync.io/docs/command-line)
* [Github Repo](https://github.com/BrowserSync/browser-sync)

Create the NPM script using the Browser Sync command line documentation:

```js
  "scripts": {
    "start": "browser-sync start --server 'app' --files 'app'"
  },
```

Or, on a Windows PC:

```js
"start": "browser-sync start --server \"app\" --files \"app\""
```

Note: Windows users should check out Microsoft's [Nodejs Guidelines](https://github.com/Microsoft/nodejs-guidelines).

And run the process:

```sh
npm run start
```

This will open index.html in your editor - examine the html and css in the inspector.

Note: Browser Sync has an interface running at port 3001.

Demo - adding a `--directory` option:

```js
  "scripts": {
    "startmac": "browser-sync start --directory --server 'app' --files 'app'",
    "startpc": "browser-sync start --directory --server \"app\" --files \"app\""
  },
```

Demo - adding a `--browser` option (note the PC browser name):

```js
"startmac": "browser-sync start --browser 'google chrome' --server 'app' --files 'app'"
"startpc": "browser-sync start --browser \"chrome.exe\" --server \"app\" --files \"app\""
```

## EXERCISE JavaScript Variables

Introducing the developer tools console, data types, variable types `var`, `let`, and `const`, and scope.

In the browser's console:

```js
var width = 100;
let wide = true;
const testString = '123456';
```

### var

* `var`can be redeclared and reassigned
* `var`is 'scoped' to a function. If a variable is defined within a function it is only available inside that function's block:

```js
function setWidth(){
  var width = 500
  console.log('inner width ' + width)
}
```

```sh
> setWidth()
> width
```

A function *does* have access to variables defined outside its block:

```js
function setWidth(){
  console.log('inner width ' + width)
}
var width = 500
setWidth()
```

Passing a parameter as an input to a function:

```js
function setWidth(num){
  var width = num || 500
  console.log('inner width ' + width)
}
setWidth(200)
setWidth()
```

* var - can 'leak' when its not inside a function:

```js
var width = 20

if ( width > 12 ) {
  var width = 4
  console.log(width)
}
```

```sh
> width
```

### let

* `let` variables can only be declared once but they can be reassigned, so this is possible:

```js
let width = 20
width = 11
```

`var` 'leaks' outside the `{ }` block.

* let and const are scoped to the block (function and otherwise - anywhere we have curly brackets)

```sh
let width = 20

if ( width > 12 ) {
  let width = 4
  console.log(width)
}

width
```

versus:

```sh
var width = 20

if ( width > 12 ) {
  var width = 4
  console.log(width)
}

width
```

`let` allows you to declare variables that are limited in scope to the block, statement, or expression in which it is used unlike the `var` keyword, which defines a variable globally, or locally to an entire function regardless of block scope.

### const

* The value of a constant cannot change through re-assignment, and it can't be redeclared.

```js
const testString = '1234abcd'
```

So these are not possible:

```js
const testString = 'abcd1234'

testString = 'xyz'
```

Note: constants are not 'immutable', they just create an immutable binding. For instance, in the case where the content is an object, the object's contents (e.g., its parameters) can be altered.

So you can still do this:

```js
const me = {
  hair: true,
  age: 48
}

me

me.age = 49

me
```

## DOM Scripting

![Image of layout](images/layout.png)

DOM scripting is not really 'pure' JavaScript. It uses JavaScript - but only in the browser - and extends vanilla JavaScript functionality with a wide variety of custom methods. The HTML DOM (Document Object Model) allows JavaScript to access and manipulate the elements of an HTML document.

See the [Mozilla Developer's Network](https://developer.mozilla.org/en-US/docs/Web/JavaScript) entry on JS and on [DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model) scripting.

## EXERCISE - generated content from an array

Note the CSS for the links:

```css
nav ul {
    list-style: none;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 2.5rem;
}

nav li {
    flex: 1;
    text-align: center;
}
```

We will replace the existing nav labels with items from an array using a `for loop`.

Examine and link to the provided JS file in index.html:

```html
<script src="js/navitems.js"></script>
```

In the console:

```js
> navItemsArray
> navItems
> typeof navItemsArray
> Array.isArray(navItemsArray)
```

Note the difference between `navItems` and `navItemsArray`. The latter contains a simple list of values while the former offers and array of objects consisting of name / value pairs.

JavaScript objects are containers for named values.

```js
var car = {type:"Fiat", model:"500", color:"white"}
```

Note that an Array is an object in JavaScript. Because an array is an object at its core you can add properties to it:

```sh
var box = []
box['size'] = 9
box['size']  // because an array is an object at its core you can add properties to it
box.size // alternate form of the syntax above
box[0] // undefined
box.push('test')
box
```

Add to the script block in the HTML:

```js
console.log(navItemsArray[2])
console.log(navItemsArray.length)
```

* DOM Method [getElementById()](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction)

```js
const nav = document.getElementById('main');
```

Alternatively we could use `querySelector()`.

* DOM Method [querySelector](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector)

```js
const nav = document.querySelector('#main');
```

But since an ID occurs only once in an HTML document it might be more efficient to let the browser know we are looking for an ID.

When you want to select multiple items use `querySelectorAll()`.

* DOM Method [querySelectorAll()](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/querySelectorAll)

```js
const navList = document.querySelectorAll('#main li a');
```

It is common to use `element.querySelector` as opposed to `document.querySelector`:

```js
const nav = document.getElementById('main');
const navList = nav.querySelectorAll('li a');
```

Leave these two lines as the only items in your script block.

Compare navList and navItemsArray in the console - Array vs nodeList types and prototypes.

A nodeList has a length property - `> navList.length` vs `> navItemsArray.length`.

Note that we have 8 items in the `navItemsArray` but only 6 in our `navList`.

### Replace our placeholder nav items with content from an array

* for loop and innerHTML

```js
for (let i=0; i < navList.length; i++ ){
  console.log(i)
  navList[i].innerHTML = navItemsArray[i];
}
```

Problem: we are using the existing `<li>` elements but there are 8 items in our `navItemsArray` array.

Solution: dynamically generate the nav from items in the array.

* depopulate the nav children

We could edit the HTML:

```html
<nav id="main"></nav>
```

Let's use JS to accomplish the same:

```js
nav.innerHTML = ''
```

Append a `<ul>` tag to nav using:

* [createElement](https://plainjs.com/javascript/manipulation/create-a-dom-element-51/) and
* [appendChild](https://plainjs.com/javascript/manipulation/append-or-prepend-to-an-element-29/)

```js
const nav = document.getElementById('main');
nav.innerHTML = ''

const navList = document.createElement('ul');
nav.appendChild(navList);
```

* dynamically create the nav based on the number of items in the array using a for loop:

```js
for (let i=0; i < navItemsArray.length; i++ ){
  let listItem = document.createElement('li')
  let linkText = navItemsArray[i]
  listItem.innerHTML = '<a href="#">' + linkText + '</a>'
  navList.appendChild(listItem)
}
```

Our nav bar now displays all the items in our array.

#### Aside - Template Strings (aka Template literals)

Compare old school concatenation and the variable 'sentence' below:

```js
  const name = 'Yorik';
  const age = 2;
  const oldschool = 'My dog ' + name + ' is ' + age * 7 + 'years old.'
  const sentence = `My dog ${name} is ${age * 7} years old.`;
  console.log(sentence);
```

Note the use of tick marks instead of quotes and that we have the ability to access variables and convert dog years to human years using JS inside the curly brackets.

#### Using [Template Strings](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)

Switch out the concatenation for a *template string*:

```js
listItem.innerHTML = `<a href="#">${linkText}</a>`
```

Since template strings accept JavaScript inside the curly braces we can further refactor to expand the use of JS:

```js
for (let i = 0; i < navItemsArray.length; i++) {
  let listItem = document.createElement('li')
  listItem.innerHTML = `<a href="#">${navItemsArray[i]}</a>`;
  navList.appendChild(listItem)
}
```

Note: template strings and `let` and `const` variables are ES6 (Ecmascript version 6). While they work on most newer browsers, they may not in older ones. For this reason it is common practice to convert the code to something more universally supported such as ES5 before publishing.

* Translate the code back to ES5 at [Babeljs.io](https://babeljs.io).

#### Aside: Objects

Open for reference: `_Objects > objects.html`

Examine the sample object in that file in the browser console:

```sh
> last
> me
> me.links
> me.links.social.twitter
```

Add to script block:

```js
const twitter = me.links.social.twitter
```

Create a multi-line template string and display it on the page:

```js
const content =
`
<div>
  <h2>
    ${me.first} ${me.last}
  </h2>
    <span>${me.job}</span>
    <p>Twitter: ${twitter}</p>
    <p>Blog: ${me.links.web.blog}</p>
</div>
`

document.body.innerHTML = content;
```

Note: this is what the above would look like without using template strings (courtesy of [Babel](https://babeljs.io)):

```js
var content = "\n<div>\n  <h2>\n    " + me.first + " " + me.last + "\n  </h2>\n    <span>" + me.job + "</span>\n    <p>Twitter: " + tw + "</p>\n    <p>Blog: " + me.links.web.blog + "</p>\n</div>\n";
```

#### Aside: Destructuring

Destructuring allows us to extract properties from objects and arrays. The curly brackets to the left of the equals sign below *do not* create an object. The destructuring assignment syntax is a JavaScript expression that makes it possible to unpack values from arrays, or properties from objects.

Add the below to objects.html:

```js
// const first = me.first;
// const last = me.last;
const { first, last } = me;
```

Access these two variables in the console:

```sh
> first
> last
```

Instead of creating multiple variables (the commented out material above), we use destructuring syntax (the curly braces) to extract information and create multiple variables. This comes in handy:

* when the data you need to access is deeply nested in an object
* when accessing third party data where you might have a variable name clash

```js
const { twitter, facebook } = me.links.social;
```

When accessing third party data where you have a variable name clash (e.g., you already have a constant variable in use called blog but you want to access content from a database that also uses that name) you can avoid issues by destructuring and renaming:

```js
const { twitter:tw, facebook:fb } = me.links.social;
```

```js
const { blog:bg } = me.links.web;
```

Our `content` variable would then be written as:

```js
const content = `
<div class="person">
  <h2>
    ${first} ${last}
  </h2>
  <span>${me.job}</span>
  <p>Twitter: ${tw}</p>
  <p>Blog: ${bg}</p>
</div>
`
```

## EXERCISE - dynamic generation with an array of objects

In the previous portion of this exercise we worked with an simple array.

An array of objects is a very common data structure.

The links for our page are in `navitems.js` - in the navItems array:

```js
var navItems = [
{
  label: 'LOGO',
  link: '#'
},
{
  label: 'Watchlist',
  link: '#watchlist'
},
{
  label: 'Research',
  link: '#research'
},
{
  label: 'Markets',
  link: '#markets'
},
{
  label: 'Workbook',
  link: '#workbook'
},
{
  label: 'Connect',
  link: '#connect'
},
{
  label: 'Desktop',
  link: '#desktop'
},
{
  label: 'FAQ',
  link: '#faq'
}
];
```

Add the links using `navItems` instead of `navItemsArray`:

```js
for (let i =0; i < navItems.length; i++ ){
  const listItem = document.createElement('li');
  listItem.innerHTML = `<a href="${navItems[i].link}">${navItems[i].label}</a>`;
  navList.appendChild(listItem);
}
```

Inspect the code and note that, thanks to the multiple name / value pairs in navItems we now have page fragment links in our html and are able to navigate within our page.

Note the hash in the url location string.

### Array Methods

Let's look at another method for developing our nav - using an Array method.

#### Array Methods: [Array.prototype.filter()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)

<!-- Refer to `_Array-methods/array-methods.html` -->

Uncomment the inventors sample data in `navitems.js`:

```js
const inventors = [
{ first: 'Albert', last: 'Einstein', year: 1879, passed: 1955 },
{ first: 'Isaac', last: 'Newton', year: 1643, passed: 1727 },
{ first: 'Galileo', last: 'Galilei', year: 1564, passed: 1642 },
{ first: 'Marie', last: 'Curie', year: 1867, passed: 1934 },
{ first: 'Johannes', last: 'Kepler', year: 1571, passed: 1630 },
{ first: 'Nicolaus', last: 'Copernicus', year: 1473, passed: 1543 },
{ first: 'Max', last: 'Planck', year: 1858, passed: 1947 },
];
```

Filter the list of inventors for those who were born in the 1500's

```js
const fifteen = inventors.filter (
  function(inventor){
    if (inventor.year >= 1500 && inventor.year <= 1599 ) {
      return true; // keep it
    }
});

console.table(fifteen);
```

##### [Arrow functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

Arrow functions are commonly used to shorten the syntax for anonymous functions. Much of the documentation you will read uses them so let start exposing ourselves to them.

Refactor using an arrow function with implicit return:

```js
const fifteen = inventors.filter(inventor => (inventor.year >= 1500 && inventor.year < 1600))
```

##### Array Methods: [Array.prototype.map()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) and [join()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/join)

Provide an array of the inventors first and last names:

```js
var fullNames = inventors.map(
  function(inventor){
  return `${inventor.first} ${inventor.last}`;
});

console.log('Full names: ' + fullNames);
```

Notice the commas separating the names.

Refactored to use an arrow function and to join the results with a comma:

```js
const fullNames = inventors.map(inventor => `${inventor.first} ${inventor.last}`).join(', ');
console.log('Full names: ' + fullNames);
```

Note the use of `join()` to add a space after the comma.

### EXERCISE - using [Array.prototype.map()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) to generate markup

An alternate method for creating the list items using map() and template strings:

```js
const markup = `
    <ul>
      ${navItems.map(
        function(navItem) {
          return `<li><a href="${navItem.link}">${navItem.label}</a></li>` }
        )}
    </ul>
    `;

console.log(markup)

nav.innerHTML = markup;
```

Join the array to avoid the comma:

```js
const markup = `
    <ul>
      ${navItems.map(
        function(navItem) {
          return `<li><a href="${navItem.link}">${navItem.label}</a></li>` }
        ).join('')}
    </ul>
    `;

nav.innerHTML = markup;
```

Refactor using an arrow function:

```js

const markup = `
<ul>
  ${navItems.map( navItem => `<li><a href="${navItem.link}">${navItem.label}</a></li>` ).join('')}
</ul>
`;

nav.innerHTML = markup;
```

Since we are including a `<ul>` in our markup constant we can remove it from our script.

Final script:

```html
<script src="js/navitems.js"></script>

<script>
const nav = document.getElementById('main');
const markup = `
    <ul>
      ${navItems.map( navItem => `<li><a href="${navItem.link}">${navItem.label}</a></li>`).join('')}
    </ul>
    `;
nav.innerHTML = markup;
</script>
```

Try translating this into ECMAScript 2015 (ECMAScript 6 / ES6) at [babeljs](babeljs.io).

## EXERCISE - Sticky Menu

Problem: the menu scrolls off the screen and we want to to be available at all times.

Solution: we will anchor the menu to the top of the screen once the user has scrolled to the point where the menu would normally be out of sight.

Note: this behavior can be managed without JavaScript using the css position property:

```css
#main {
  position: sticky;
  top: 0px;
}
```

I have elected not to do so because not only is it useful to understand position in JavaScript, but also because it is common to make other changes to the DOM contingent on other changes.

The DOM method [`offSetTop`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/offsetTop) allows us to get information about the position of an element relative to the top of the browser's window.

(See also [`getBoundingClientRect`](https://developer.mozilla.org/en-US/docs/Web/API/Element/getBoundingClientRect) which returns much more information and is incredibly useful for all manner of positioning).

```js
let topOfNav = nav.offsetTop;
```

The DOM method - [addEventListener('event', function)](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener), see also [event types](https://developer.mozilla.org/en-US/docs/Web/Events) allows us to listen for an event in the browser and run a function when it occurs.

```js
window.addEventListener('scroll', fixNav);
```

Use [window.scrollY](https://developer.mozilla.org/en-US/docs/Web/API/Window/scrollY) to get the number of pixels that the document is currently scrolled vertically:

```js
function fixNav() {
  console.log(topOfNav)
  console.log(window.scrollY)
}
```

When `topOfNav` is equal to `window.scrollY` we want to use CSS to make the menu stay at the top of the screen.

To do so we'll employ [classList](https://plainjs.com/javascript/attributes/adding-removing-and-testing-for-classes-9/):

```js
function fixNav() {
  if(window.scrollY >= topOfNav) {
    document.body.classList.add('fixed-nav');
  }
}
```

And add the css for the `fixed-nav` class:

```css
body.fixed-nav nav {
  position: fixed;
  top: 0;
  box-shadow:0 5px 3px rgba(0,0,0,0.1);
  width: 100%;
  z-index: 1;
}
```

And test in the browser.

Add an `else` to our `if` statement to remove the sticky behavior when the banner image is showing.

```js
function fixNav() {
  if(window.scrollY >= topOfNav) {
    document.body.classList.add('fixed-nav');
  } else {
    document.body.classList.remove('fixed-nav');
  }
}
```

We added the class `fixed-nav` to the html body tag (as opposed to, say, the nav itself) so that we can use it to target other elements on the page which may not be children of the nav. Let's do this with the site-wrap.

```css
.site-wrap {
  max-width: 780px;
  margin: 40px auto;
  background:white;
  padding:40px;
  text-align: justify;
  box-shadow: 0 0 10px 5px rgba(0, 0, 0, 0.05);
  /* add these two */
  transform: scale(0.98);
  transition: transform 0.5s;
}
```

```css
body.fixed-nav .site-wrap {
  transform: scale(1);
}
```

When the nav gets position fixed it no longer takes up space in the window so the content beneath it jumps upward (reflows).

Take care of this jump using `offsetHeight` to add an amount of padding equal to the height of the nav to the body element.

```js
function fixNav() {
  if(window.scrollY >= topOfNav) {
    document.body.style.paddingTop = nav.offsetHeight + 'px';
    document.body.classList.add('fixed-nav');
  } else {
    document.body.classList.remove('fixed-nav');
    document.body.style.paddingTop = 0;
  }
}
```

Note `paddingTop` (camel case) - I used Javascript for this because the height of the nav bar (`offSetHeight`) could vary. Otherwise I would have used the CSS file. Always try to use CSS instead of Javascript wherever possible.

## EXERCISE - Adding the SVG Image

```js

const logo = document.querySelector('#main ul li');
logo.classList.add('logo');
logo.firstChild.innerHTML = '<img src="img/logo.svg" />';
```

* Examine the SVG file
* some interesting applications of SVG:

[Responsive logos](http://responsivelogos.co.uk)

[Background generator](http://www.svgeneration.com/recipes/Beam-Center/)

Format the logo and create the sliding logo behavior. Note: CSS only, no JavaScript:

```css
li.logo img {
  padding-top: 0.25rem;
  width: 2.5rem;
}

li.logo {
  max-width:0;
  overflow: hidden;
  background: white;
  transition: all 0.5s;
  font-weight: 600;
  font-size: 30px;
}

.fixed-nav li.logo {
  max-width:500px;
}
```

(Note the use of max-width above. We are using this because transitions do not animate width.)

## EXERCISE - Faking It

Note the use of hashes in the navigation:

`<a href="#watchlist">Watchlist</a>`

These allow us to navigate (`index.html#research`) to sections of the document marked up with the corresponding id:

`<p id="watchlist">`

Note that clicking on an hashed link doesn't refresh the page. This makes hashes an important feature for creating SPAs - they are used to load different content via AJAX from a server with no page refresh.

We'll set up our page emulate a single page application.

Run `window.location` in the console.

Sample of a page fragment redirect using `setTimeout()`:

```js
window.onload = function(){
  window.location.hash = '#'
  setTimeout( () => window.location.hash = '#watchlist' , 1500)
}
```

Delete the code above.

```js
const navTest = document.querySelectorAll('#main ul li a');
for (let i=0; i<navTest.length; i++){
  console.log('hash ', navTest[i].hash);
}
```

Add an event listener to the links in the nav:

```js
const navTest = document.querySelectorAll('#main ul li a');
for (let i=0; i<navTest.length; i++){
  navTest[i].addEventListener('click', prepContent)
}

function prepContent(e){
  if (this.hash == "#workbook"){
    e.preventDefault();
  }
}
```

We have hijacked the normal functioning on the workbook link.

Let's use the fakeContent provided in our sample data file for the content of a new variable `siteWrap`. Update the script above to:

1. create a reference to `site-wrap`
1. access fake header and content from the `navitems.js` array
1. use `innerHTML` to apply that content to the document

```js
const sitewrap = document.querySelector('.site-wrap');
const navTest = document.querySelectorAll('#main ul li a');
for (let i=0; i<navTest.length; i++){
  navTest[i].addEventListener('click', prepContent)
}

function prepContent(e){
  if (this.hash == "#workbook"){
    const header = fakeContent[0].header;
    const content = fakeContent[0].content;
    sitewrap.innerHTML = `
      <h2>${header}</h2>
      <p>${content}</p>
    `;
    e.preventDefault();
  }
}
```

### Notes

[vh and vw in CSS](https://css-tricks.com/viewport-sized-typography/)

#### OLD HW - CSS Flexible Box Layout Module

Flexbox can be quite difficult to master. You could do worse than checking out:

* Free Code Camp's [article on Medium.com](https://medium.freecodecamp.com/understanding-flexbox-everything-you-need-to-know-b4013d4dc9af#.usjz1l93w), or

* A simple guide to the various CSS properties on [CSS Tricks](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

`<img src="other/hero-1.png">`

[Use a system font instead of a custom font?](https://www.smashingmagazine.com/2015/11/using-system-ui-fonts-practical-guide/) [In SVG?](https://css-tricks.com/system-fonts-svg/)

```css
body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto", "Oxygen", "Ubuntu", "Cantarell", "Fira Sans", "Droid Sans", "Helvetica Neue", sans-serif;
}
```

```css
.site-nav ul {
  list-style: none;
  display: flex;
  margin: 0;
  padding: 0;
}

.site-nav li {
  width: 100px;
  height: 100px;
  background-color: #8cacea;
  margin: 8px;
}
```

```css
.account-dropdown ul {
  display: none;
}

.site-header {
  background: #0D1313;
  color: white;
  display: flex;
  align-items: center;
  padding:0.5rem;
}

.logo {
  text-decoration: none;
  color: white;
  font-size: 0.9rem;
  text-transform: uppercase;
  letter-spacing: 3px;
  padding: 10px;
}

a {
  text-transform: uppercase;
  text-decoration: none;
  color: #CDD0D0;
  padding: 20px;
  display: inline-block;
}

.active a {
  font-weight: bold;
  color: #62DEBE;
  background: darken(#62DEBE, 40%);
}

.account-actions {
  margin-left: auto;
  display: flex;
  align-items: center;
  margin-right: 10px;
}

.sign-out-link {
  color: #62DEBE;
  font-size: 0.8rem;
  margin-left: 10px;
  text-transform: uppercase;
}

@media (max-width: 600px) {
  .site-header {
    flex-wrap: wrap;
  }
  .site-nav {
    order: 2;
    background: #333;
    width: 100%;
  }
}
```

[Font Awesome](http://fontawesome.io/)

```html
<link rel="stylesheet" href="font-awesome-4.6.3/css/font-awesome.min.css">

<i class="fa fa-bullseye fa-3x"></i>

<i class="fa fa-gear"></i>

```

Comment out the contents of the ul:

```html
<nav class="site-nav">
  <ul>
    <!-- <li class="active"><a href="#0">Recipes</a></li>
    <li><a href="#0">Reviews</a></li>
    <li><a href="#0">Delivery</a></li> -->
  </ul>
</nav>
```

```html
<div class="site-wrap">
  <h4>Homework</h4>

  <p>The items below all come from today's work on the Basic DOM scripting page. You should attempt each one if possible.</p>

  <ol>
    <li>Create an object with a new set of labels and links for the site-nav li's above and use the JavaScript techniques we covered today to dynamically generate the nav menu</li>

    <li>Use classList to assign the active class to a link when clicked (be sure to remove it from the previously highlighted link as well)</li>

    <li>Add some paragraphs to the page and make the navigation sticky</li>
  </ol>

  <p>Post your efforts to the class Slack Channel and a web server (if you don't have I can provide)</p>
</div>
```

##### ALT loader

```js
function loadDoc1() {
  var xhttp = new XMLHttpRequest();
  xhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
      document.getElementById(“textbox”).innerHTML =
      this.responseText;
    }
  };
  xhttp.open(“GET”, “texts/latestnews.html”, true);
  xhttp.send();
}
```

```html
<nav>
  <ul class=“nav”>
    <li class=“latestnews”><a href=“#” onclick=“loadDoc1()“>LATEST NEWS</a></li>
    <li class=“eswnyc”><a href=“#” onclick=“loadDoc2()“>ESW-NYC</a></li>
    <li class=“team”><a href=“#” onclick=“loadDoc3()“>TEAM</a></li>
    <li class=“projects”><a href=“#” onclick=“loadDoc4()“>PROJECTS</a></li>
    <li class=“contactus”><a href=“#” onclick=“loadDoc5()“>CONTACT US</a></li>
    <li class=“participate”><a href=“#” onclick=“loadDoc6()“>PARTICIPATE</a></li>
    <li class=“donate”><a href=“#” onclick=“loadDoc7();“>DONATE</a></li>
  </ul>
</nav>

```


petitagneaunoir@gmail.com, yumi.ishizuka@gmail.com, paul@instoresnowhere.com, clj260@nyu.edu, am4970@nyu.edu, pavitranew@gmail.com, brs358@nyu.edu