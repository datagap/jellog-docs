# Figures

`jellog-figure` is the main container for bootstrap figure items. 

Basic usage:

````html
<jellog-figure>
  <jellog-image src="..." class="img-fluid rounded" alt="A generic square placeholder image with rounded corners in a figure.">
  <jellog-figcaption class="text-end">A caption for the above image.</jellog-figcaption>
</jellog-figure>
````

It adds `figure` class to main container, also adds `figure-img` class to inner `jellog-image` element and `figure-caption` class to inner `jellog-figcaption` element.