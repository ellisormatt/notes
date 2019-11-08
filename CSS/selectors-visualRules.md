# linking the CSS file
```html
<link href="./style.css" type="text/css" rel="stylesheet">
```
# tag names
```css
p {
    font-family: Arial;
}
```
- makes all **p** elements use Arial in the section in which the stylesheet is linked
# class names
- for the following HTML:
```html
<p class="brand">Sole Shoe Company</p>
```
- class attribute set to "brand"
- to select this elemend using CSS:
```css
.brand {

}
```
- you can also use multiple classes to target a single HTML element:
```css
.green{
    color: green;
}
.bold {
    font-weight: bold;
}
```
```html
<h1 class="green bold"> ... </h1>
```
# ID Name
```html
<h1 id="large-title"> ... </h1>
```
- in CSS to select an element by its ID attribute:
```css
#large-title {

}
```
# chaining selectors
```css
h1.special{

}
```
- special class for h1 elements
# nested elements
```html
<ul class="main-list">
    <li></li>
    <li></li>
</ul>
```
```css
.main-list li {

}
```
- .main-list selects the main-list element, by adding li, the nested li elements are selected as well
# important
```css
p {
    color: blue !important;
}
.main p {
    color: red;
}
```
- important overrides any other spfcificity
# multiple selectors
```css
h1 {
    font-family: Georgia;
}
.menu {
    font-family: Georgia;
}
```
- can be rewritten as:
```css
h1,.menu {
        font-family: Georgia;
    }
```
# background image
```css
.main-banner {
    background-image: url("https://www.example.com/image.jpg");
}
```
