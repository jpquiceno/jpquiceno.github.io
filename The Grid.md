#Death to the Table or: How I Learned to Stop Worrying and Love the Grid
--
In the very beginning, there were no style sheets,…at least, not for authors. This meant that their was very little in the way of changing the look of a web page. Hyper Text Markup Language (HTML) was never intended to do more than contain content for a web page. 

By the mid 90's cutting edge web designers were hacking tables to produce some great layouts.  This involved slicing images up into little squares that were laid into the tables to create some customization.  This allowed for some unexpected positive results, such as: fluid and responsive designs.  The industry soon realized that tables should be used as they were originally intended for, tabular data.  This required a better solution for creating graphical layouts, Cascading Style Sheets (CSS) was the answer.

####[TL;DR](#tldr)

###A brief history of CSS:

In October 1994, Tim Berners-Lee formed the World Wide Web Consortium, (W3C) at the Massachusetts Institute of Technology Laboratory for Computer Science.  The W3C is made up of members representing all sort of institutions including: government, educational, business and individuals. This organization is responsible for making recommendations which are used to keep the experience consistent across all browsers.

Hakon Wium Lie released the first draft of “Cascading HTML Style Sheets” in October 1994. After 9 separate proposals were presented to the W3C, influenced the creation of CSS.  It would become in important to support additional markup languages so, HTML was removed from the name. In late 1995, the W3C set up an Editorial Review Board to make HTML specifications.

In December on 1996 CSS level 1 was released. It supported: font properties, text attributes, alignment of text, tables, images and more, colors of text and backgrounds, spacing of words, letters and lines, margins, borders, padding and positioning, and unique identification and classification of groups of attributes.

W3C released CSS 2 in May of 1998 which added new capabilities including z-index, media types, bidirectional text, absolute, relative and fixed positioning, and support for aural style sheets.  By June 2011 that W3C released CSS 2.1, which fixed errors and aligned the capabilities better with browser functions.

With the release of CSS 3, its capabilities were separated into modules.  The following modules were released as formal recommendations: color, selectors level 3, namespaces and media queries. This means that future releases of CSS will be released in smaller specifications due to the modularization of CSS 3.

So this all leads to today and how we have come full circle, back to table layouts, without the use of tables.  How you ask?  Well, allow me to introduce the Grid.   

###<a id="tldr"></a>CSS Grid Layout

The [CSS Grid layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout/Basic_Concepts_of_Grid_Layout) is a layout method that arranges a web page's items in two dimensional layout. While others, like Flexbox, arranges layouts in one dimension.  This resolves the issue of not being able to achieve both a vertical and horizontal alignment.  This is what makes CSS Grid a powerful solution.

####Additional Benefits:

* **Versatile** in how layouts can be constructed, being adaptable in varying combinations of rows and columns. They even support nested grids for more complex use cases. No matter your layout requirements, a grid system is almost certainly well suited.

* **increase in productivity** by providing simple and predictable layout scaffolding to HTML design. The structure of a page can be formulated quickly without second guessing its precision or cross-browser compatibility.

* **Ideal for responsive layouts** This is where grid systems reign supreme. They make it incredibly easy to create mobile friendly interfaces that are adaptable to different sized viewports.

Support for CSS Grid is widely supported by most of the major browsers with the exception of IE Edge, which is out dated and supports an older version of the specification according to [caniuse.com](http://caniuse.com/#feat=css-grid).  Grid has been in development for over 5 years now, though behind a flag.  This was done to help prevent a buggy launch like Flexbox had.

I would be remiss if I did not mention [Rachel Andrew](https://twitter.com/Rachelandrew) here, a technology expert and recognized authority of CSS. A [GDE](https://developers.google.com/experts/people/rachel-andrew) \(Google Developers Expert\).  Rachel has a great website and a valuable resource for getting familiar with the grid, [Grid by Example](https://gridbyexample.com/).

###Defining a grid

In our example we take a look at a 12-column grid layout, which happens to be a very popular layout. Since 12 is divisible by 2, 3, 4 and 6, this makes for a useful layout amongst web designers.

The base markup starts as follows:

~~~html
<!DOCTYPE html>
<body>
	<div class="wrapper">
		<header class="box">Header</header>
		<nav class="box">Nav</nav>
		<main class="box">Main Area</main>
		<footer class="box"></footer>
	</div>
</body>
~~~

<!--![Image placeholder](/Users/jean-paulquiceno/Desktop/477291-54-635993123236628816_338x600_thumb.jpg "Image placeholder")-->

From here we will create a 2 columns layout for simplicity. Our layout will consist of 3 rows, the first contains the header column.  The second row will share 2 columns, the navigation and the main content. Lastly, the column footer will be in the remaining row.

To define a Grid use `display:grid` or `display:inline-grid` on the parent element. You can then create a grid using the `grid-template-columns` and `grid-template-rows` properties, which are called tracks.

Let's start by creating some white space on the body and adding a wrapper to expand it so covers the entire viewport, while making it into a grid container. Now we can define our first set of tracks, the rows: 

~~~markup
body {
  margin: 40px;
}
.wrapper {
  display: grid;
  grid-template-rows: 75px auto 50px;
}
~~~

We will now set up a series of sizes to define the individual rows using `grid-template-rows`.  In our example, we are setting the first row height to 75px and the last one to 50px.  The remaining middle row is set to `auto` which permits the height to adjust as needed to accommodate *the grid items*.

Our second set of tracks consist of columns.  Now let's make the columns more dynamic. We want the nav and main area to shrink and grow, while always maintaining a minimum width of 150px and also keeping the main area larger than the nav.  The class `.box` is used to create a base of colors and font sizes

~~~html
.wrapper {
  display: grid;
  grid-template-rows: 75px auto 50px;
  grid-template-columns: minmax(150px, 2fr) 8fr;
}
.box {
  background-color: #444;
  color: #fff;
  padding: 20px;
  font-size: 120%;
}
~~~

The CSS above is setting a minimum and maximum size of that track. The minimum width is 150px, while the maximum width is `2fr`.  The `fr` is grid-specific unit that allows distribution of available space to the frid elements. The main area is set to 4 times the width of the navigation column.


I am using the `grid-gap` property to create a gap between my columns and rows of 10px. This property is a shorthand for `grid-column-gap` and `grid-row-gap` so you can set these values individually.  All direct children of the parent now become grid items and the auto-placement algorithm lay them out, one in each grid cell.  Creating extra rows as needed.

~~~html
.wrapper {
  display: grid;
  grid-template-rows: 75px auto 50px;
  grid-template-columns: minmax(150px, 2fr) 8fr;
  grid-gap: 10px;
}
~~~

The remaining elements only require the using a shorthand syntax declaring the start and end values at once. Values are separated with a / and again it would be valid to omit the / and the end value as we are spanning only one track.

~~~html
header {
    grid-column: 1 / 3;
}
nav {
    grid-row: 2;
    grid-column: 1 / 2;
}
main {
    grid-row: 2;
    grid-column: 2 / 3;
}
footer {
    grid-column: 1 / 3;
}
~~~

The header and the footer are both set to start at 1 and end at 3. While the navigaton is set to start at 1 and end at 2.  Lastly, the main area is set to start at 2 and end at 3.  Below you can see the final layout example.

<p data-height="296" data-theme-id="0" data-slug-hash="RgLpvM" data-default-tab="result" data-user="Japes" data-embed-version="2" data-pen-title="Defining a Grid" class="codepen">See the Pen <a href="https://codepen.io/Japes/pen/RgLpvM/">Defining a Grid</a> by Jean-Paul Quiceno (<a href="https://codepen.io/Japes">@Japes</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

###Where to go from here?
We are at an exciting time with the advent of CSS Grid layout.  As you can see setting up a responsive layout is the perverbial, piece of cake.  Now designers have the ability to create layouts as we did in the 90's without having to resort to using tables.  And it works accross most of the major browsers. Now you can have your cake and eat it too.







