# header and nav
```html
<header></header>
replaces
<div id="header></div>
```
```html
<nav></nav>
replaces
<div id="header"></div>
```
# main and footer
```html
<main></main>
```
- used to encapsulate the dominant content within a webpage
```html
<footer></footer>
```
- contains info such as contact info, copyright, terms of use, site map, etc

# section and article
```html
<section>
    <h2>Some info about something</h2>
    <article>
        <p>some more specific information about somt thing that is somewhat related to the section</p>
    </article>
</section>
```
<section>
    <h2>Some info about something</h2>
    <article>
        <p>some more specific information about somt thing that is somewhat related to the section</p>
    </article>
</section>

# aside 
```html
<article>
    <p>some paragraph about things about a topic</p>
</article>
<aside>
    <p>some aside tangentially related to the contant above?</p>
</aside>
```
- uses for aside include: bibliographies, endnotes, comments, pull quotes, sidebars, etc

# figure and figcaption
```html
<figure>
    <img src="somewebsite.com/somepicture.jpg">
    <figcaption>this picture is somepicture i found on somewebsite</figcaption>
</figure>
```
- figure is an element used to encapsulate media such as an image
- figcaption describes media in the *figure* tag

# audio and attributes
```html
<audio autoplay controls>
    <source src="someAudioFile.mp3" type="audio/mp3">
</audio>
```

# video and embed
```html
<video src="video.mp4" controls>text that shows when video fails to load</video>
<embed src="somegif.gif"/>
```
