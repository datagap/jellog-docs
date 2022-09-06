# Cards

## Introduction

`jellog-card` is a content container derived from bootstrap card element.

Basic usage:

````xml
<jellog-card style="width: 18rem;">
  <img jellog-card-image="Top" src="~/imgs/demo/300x200.png"/>
  <jellog-card-body>
    <jellog-card-title>Card Title</jellog-card-title>
    <jellog-card-text>Some quick example text to build on the card title and make up the bulk of the card's content.</jellog-card-text>
    <a jellog-button="Primary" href="#"> Go somewhere</a>
  </jellog-card-body>
</jellog-card>
````



##### Using Titles, Text and Links: 

Following tags can be used under main `jellog-card` tag

* `jellog-card-title`
* `jellog-card-subtitle`
* `a jellog-card-link`

Sample:

````xml
<jellog-card style="width: 18rem;">
    <jellog-card-body>
       <jellog-card-title>Card title</jellog-card-title>
       <jellog-card-subtitle class="mb-2 text-muted">Card subtitle</jellog-card-subtitle>
       <jellog-card-text>Some quick example text to build on the card title and make up the bulk of the card's content.</jellog-card-text>
       <a jellog-card-link href="#">Card link</a>
       <a jellog-card-link href="#">Another link</a>
    </jellog-card-body>
</jellog-card>
````



##### Using List Groups:

* `jellog-list-group flush="true"` : `flush` attribute renders into bootstrap `list-group-flush` class which is used for removing borders and rounded corners to render list group items edge to edge in a parent container.
* `jellog-list-group-item`

Kitchen Sink Sample:

````xml
<jellog-card style="width: 18rem;">
    <img jellog-card-image="Top" src="~/imgs/demo/300x200.png" />
    <jellog-card-body>
       <jellog-card-title>Card Title</jellog-card-title>
       <jellog-card-text>Some quick example text to build on the card title and make up the bulk of the card's content.</jellog-card-text>
    </jellog-card-body>
    <jellog-list-group flush="true">
       <jellog-list-group-item>Cras justo odio</jellog-list-group-item>
       <jellog-list-group-item>Dapibus ac facilisis in</jellog-list-group-item>
       <jellog-list-group-item>Vestibulum at eros</jellog-list-group-item>
    </jellog-list-group>
    <jellog-card-body>
       <a jellog-card-link href="#">Card link</a>
       <a jellog-card-link href="#">Another link</a>
    </jellog-card-body>
</jellog-card>
````



##### Using Header, Footer and Blockquote:

* `jellog-card-header`
* `jellog-card-footer`
* `jellog-blockquote`

Sample:

```xml
<jellog-card style="width: 18rem;">
    <jellog-card-header>Featured</jellog-card-header>
    <jellog-card-body>
       <jellog-card-title> Special title treatment</jellog-card-title>
       <jellog-card-text>With supporting text below as a natural lead-in to additional content.</jellog-card-text>
       <a jellog-button="Primary" href="#"> Go somewhere</a>
    </jellog-card-body>
</jellog-card>
```

Quote Sample:

```xml
<jellog-card>
    <jellog-card-header>Quote</jellog-card-header>
    <jellog-card-body>
<jellog-blockquote>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer posuere erat a ante.</p>
    <footer>Someone famous in Source Title</footer>
</jellog-blockquote>
    </jellog-card-body>
</jellog-card>
```

Footer Sample:

```xml
<jellog-card class="text-center">
    <jellog-card-header>Featured</jellog-card-header>
    <jellog-card-body>
        <jellog-blockquote>
            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer posuere erat a ante.</p>
            <footer>Someone famous in Source Title</footer>
        </jellog-blockquote>
    </jellog-card-body>
    <jellog-card-footer class="text-muted"> 2 days ago</jellog-card-footer>
</jellog-card>
```



## Demo

See the [cards demo page](https://bootstrap-taghelpers.jellog.io/Components/Cards) to see it in action.

## jellog-card Attributes

- **background:** A value indicates the background color of the card.
- **text-color**: A value indicates the color of the text inside the card.
- **border:** A value indicates the color of the border inside the card.

Should be one of the following values:

* `Default` (default value)
* `Primary`
* `Secondary`
* `Success`
* `Danger`
* `Warning`
* `Info`
* `Light`
* `Dark`

Example:

````xml
<jellog-card background="Success" text-color="Danger" border="Dark">
````

### sizing

Cards has default 100% with and can be changed with custom CSS, grid classes, grid Sass mixins or [utilities](https://getbootstrap.com/docs/4.0/utilities/sizing/).

````xml
<jellog-card style="width: 18rem;">
````

### card-deck and card-columns

`jellog-card` can be used inside `card-deck` or `card-columns` aswell.

````xml
<div class="card-deck">
    <jellog-card background="Primary">
        <jellog-card-header>First Deck</jellog-card-header>
        <jellog-card-body>
            <jellog-card-title> Ace </jellog-card-title>
            <jellog-card-text>Here is the content for Ace.</jellog-card-text>
        </jellog-card-body>
    </jellog-card>
    <jellog-card background="Info">
        <jellog-card-header>Second Deck</jellog-card-header>
        <jellog-card-body>
            <jellog-card-title> Beta </jellog-card-title>
            <jellog-card-text>Beta content.</jellog-card-text>
        </jellog-card-body>
    </jellog-card>
    <jellog-card background="Warning">
        <jellog-card-header>Third Deck</jellog-card-header>
        <jellog-card-body>
            <jellog-card-title> Epsilon </jellog-card-title>
            <jellog-card-text>Content for Epsilon.</jellog-card-text>
        </jellog-card-body>
    </jellog-card>
</div>
````
