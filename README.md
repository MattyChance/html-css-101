HTML & CSS: 101
===============

## From HTTP to HTML
Last week, we focused on the HTTP protocol.  Using NodeJS and Express, we created a web server, or HTTP server. Our server was able to respond to requests to different URLs with appropriate responses. Often, these responses were in the form of HTML documents.

To send an HTML document to a browser, a web server will send the text of the HTML document in the **body of the HTTP response**. If it's a good server, it will also include an **http header** of `Content-Type: text/html` to let the browser know that the content in the text document being transfered is HTML.

Upon receiving a text document that is detected as HTML, the browser will treat the document in a special way: it will parse it using a set of rules, and draw -- or **render** -- the HTML document.

## Parsing HTML: the DOM
HTML is a text along with tags giving special meaning to this text. For the browser to be able to do anything with an HTML document, it first has to **parse the document**, and create an **internal structure** called the DOM, or **Document Object Model**: an object-based model of the HTML document.

One way to inspect the structure created by the browser is to use the Dev Tools. Each browser has its own development tools, but they mostly have the same functionalities. Among other things, the Dev Tools will allow us to inspect the DOM, but also to run JavaScript in the context of the web page as well as view network requests.

More often than not, the DOM structure looks just like the HTML that was parsed by the browser but sometimes it can differ. For example, with the following HTML:

```html
<h1>Hello World!</h1>
<p>This is some text</p>
```

the browser's Dev Tools will display the following DOM:

![dev tools DOM](https://s11.postimg.org/6nhc8o0ir/Screen_Shot_2016_10_30_at_22_17_56.png)

Notice that our HTML did not have the `<html>`, `<head>` nor `<body>` tags. When the browser parsed our HTML document into the DOM structure, it had to fill in the blanks and create missing elements in order to have a complete DOM.

In addition to parsing our HTML, creating the DOM and rendering the web page, our browser will download any resources linked to from our HTML document. These could be images added with the `<img>` tag, stylesheets added with the `<link>` tag or browser JavaScript added with the `<script>` tag.

Images will be rendered along with the web page, stylesheets will be used to determine the appearance of the web page, and JavaScript will be used to create interactivity within the web page.

## Box All The Things!
If we use the Dev Tools inspector, we can see that everything in our HTML document is seen by the browser as a box.

Even elements that don't look like boxes -- be it because they have a transparent background or because they look circular -- are actually boxes. Here's an example of inspecting a circular-looking image in Chrome Dev Tools:

![circular-looking image in dev tools](https://s12.postimg.org/j2d4kcx6l/Screen_Shot_2016_10_30_at_22_46_46.png)

As we'll see in the next sections, we can use this box model to our advantage when creating our HTML pages.

## Boxifying a design
Let's say that you just received a design from the in-house designer at the company you worked for. It's for a customer who breeds flying kittens. The design looks like this:

![pdf design to html](https://s17.postimg.org/tytvbzcxb/Screen_Shot_2016_10_30_at_23_07_08.png)

The first thing you should do when receiving such a design is to boxify it. Draw a box around anything that could be an element, as long as it makes sense. For example, your boxification could look like this:

![boxified psd template](https://s15.postimg.org/utz2ehjwr/Screen_Shot_2016_10_30_at_23_07_08.png)

## From boxes to `<div>`s
Notice that just like the DOM, our exercise produced nested boxes. For this step, let's start by creating the structure of our document, using a `<div>` tag for every box we drew on the page. Since we don't have the images and the final text yet, we'll use placeholders for the moment. We'll take care of the social icons later too, and just use text for now.

Our final HTML should look like this:

```html
<div>Flying Kittens! Inc.</div>
<div>
  <div>
    image of flying kitten
  </div>
  <div>
    description text about Flying Kittens! Inc.
  </div>
</div>
<div>
  <div>&copy; 2016 Flying Kittenz! Inc.</div>
  <div>
    facebook
  </div>
  <div>
    twitter
  </div>
  <div>
    youtube
  </div>
</div>
```

Opening this HTML file in the browser, it looks nothing like the design. Let's go back and create a full HTML document, and link it to an empty `styles.css` stylesheet. We'll talk about styling in more detail next.

Our HTML should look like this:

```html
<!doctype html>
<html>
<head>
  <title>Flying Kittens! Inc.</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
<div>Flying Kittens! Inc.</div>
<div>
  <div>
    image of flying kitten
  </div>
  <div>
    description text about Flying Kittens! Inc.
  </div>
</div>
<div>
  <div>&copy; 2016 Flying Kittenz! Inc.</div>
  <div>
    facebook
  </div>
  <div>
    twitter
  </div>
  <div>
    youtube
  </div>
</div>
</body>
</html>
```

## More on CSS
If HTML describes the structure of a document, then CSS describes its appearance. Separating the two concerns makes it easier to create maintainable web pages, and makes changes to the appearance of the pages easier.

It's pretty much impossible to learn everything about CSS. The specification is huge, and contains huge sections that we don't use every day. This introduction will give you an overview of the important aspects of CSS.

### Separating appearance from structure
First off, if you want to convince yourself of the power of CSS, and of separating the HTML structure from its appearance, take a look at [CSS Zen Garden](http://csszengarden.com/). This site lists a series of CSS designs that look wildly different, but are all based on the exact same HTML structure.

The awesome power of CSS has not always been present for web developers, who in the past have had to rely on HTML tags like `<font>` and attributes like `bgcolor` for styling. **With CSS, there is no reason to use HTML as a way to style a document.** This will become clearer when we talk about semantic HTML elements.

### Selectors and declarations
In CSS, we use **selectors** to target the HTML elements we want to style. The most common type of selector is the **class selector**. To use it, we add a `class` attribute to an HTML element, which represents what the element is about. Then, we use this same class name prefixed with a dot `.` to target it in our CSS, and give it some styles. What styles to give to an element is something that you learn with practice. This lesson will show you some of the most common styling recipes, but the list is too long to show all of them.

If we want to select all elements of the same type -- or tag --, we can simply select them by writing out the name of the element.

Once we know which elements we want to select, we can write one or more **declarations** which will apply to the selected elements. A declaration is one line of CSS, which contains a property and a value separated by a `:`. The declaration ends with a `;`.

Here is an example where we select all `<a>` elements on the page, and make their text color red as well as their font weight bold:

```css
a {
    color: red;
    font-weight: bold;
}
```

Here we are using `a` as the selector because we want to target all `<a>` elements.

Here is an example where we select all elements with the `title` class,  make their font size twice as large as the current font size and give them a noticeable bottom margin:

```css
.title {
    font-size: 2em;
    margin-bottom: 0.3em;
}
```

We can give the same style to multiple selectors by listing them separated by a `,`. For example, if we want all headings of our page to use the same font:

```css
h1, h2, h3, h4, h5, h6 {
    font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
    font-weight: 400;
    color: #222;
}
```

### The Box Model
As mentioned earlier, the browser sees everything on the page as a box. The browser has some properties that it associates to each box. We can see these box model properties when we open the dev tools and inspect an element:

![box model in dev tools](https://s15.postimg.org/67czqeud7/Screen_Shot_2016_10_30_at_23_33_03.png)

Here is a description of each property and what it does:

* Content size (in blue): This inner-most represents the size of the content. As we'll see, boxes will take all the horizontal space of their parent by default, and their height will be determined by the content that flows inside. We can also use the `width`, `height`, `min-width`, `min-height`, `max-width` and `max-height` to give the browser directions about the desired size of a box. These values can be specified in `px` or `%`.
* Padding (in green): The padding represents breathing space around the content, and comes right before the border. Any background applied to an element will extend to its padding. Padding can be controlled with the `padding` property, or by specifying the padding of each side separately with `padding-left`, etc.
* Border (in yellow): The border represents a visible border around the element. The shorthand `border` property allows us to specify the width, type and color of the border using one CSS declaration only. For example, a `border` of `1px solid black` will create a one-pixel solid black border all around the targeted box.
* Margin (in orange): The margin represents breathing space outside of an element, and comes right after the border. Any backgrounds applied on an element will *NOT* extend to its margin, allowing the margin to be used to separate two elements from each other. The margin can be set all around with the `margin` property, or for each side using `margin-left`, etc.

### The Box Sizing Calculation
By default, when you specify the `width` or `height` of an element, the browser will *exclude* the width of the `border` and `padding` in the calculation of the width. Therefore, if you give a box a `width` of `200px` and a `padding` of `10px`, the box will *NOT* be `200px` wide but `220px`, which is `200px + 10px for left padding + 10px for right padding`.

This default sizing behavior is called "content box sizing". It makes reasoning about the size of elements difficult. For this reason, when starting a new design from scratch it is advised to use the alternative box sizing mode of "border box". With border box, the width and height calculations *include* the padding AND the borders. Setting a `width` of `200px` on an element using border-box, the element will always be `200px` wide. If it has more padding or border, then there will just be less space for the content.

To apply border-box sizing across all your page in the least destructive format, use the following bit of CSS at the top of your stylesheet:

```css
html {
  box-sizing: border-box;
}
*, *::before, *::after {
  box-sizing: inherit;
}
```

### The CSS Cascade
The "C" in CSS refers to the cascade, a set of rules used to determine which CSS will apply to an element. Since CSS can declare multiple style rules that end up applying to the same elements, the browser has to determine which rule "wins". This process is referred to as the cascade. Here's an example:

```css
h1 {
    font-family: "Helvetica Neue";
}

.title {
    font-family: "Comic Sans";
}
```

```html
<h1 class="title">This is a title</h1>
```

With the previous HTML and CSS, it's clear that the `h1` element is targeted both by the `h1` type selector as well as the `.title` class selector. Which font will this h1 have? It turns out that since **class selectors are more specific than type selectors**, this `h1` will have the Comic Sans font applied to it.

What if the `h1` had two class names such as `"title big"` -- class names are spearated by a space -- and the following CSS:

```css
h1 {
    font-family: "Helvetica Neue";
}

.title {
    font-family: "Comic Sans";
}

.big {
    font-family: "Impact";
}
```

```html
<h1 class="title big">This is a title</h1>
```

In this case, there are three conflicting rules. The `h1` rule loses because it's less specific, but the two class selectors have the same **specificity**. In this case, the one that comes later in the source code wins. This `h1` will have a font of Impact because the rule for `.big` comes after the rule for `.title` in the source of the CSS.

Read the MDN documentation on [CSS Cascade](https://developer.mozilla.org/en-US/docs/Web/CSS/Cascade) and [Specificity](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity) to get all the details.

## Layouts 101
Let's start using some CSS to make our web page look closer to the design. First off, let's add some class names to our HTML elements:

```html
<!doctype html>
<html>
<head>
  <title>Flying Kittens! Inc.</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
<div class="title">Flying Kittens! Inc.</div>
<div class="main-section">
  <div class="image">
    <img src="http://placekitten.com/g/401/401">
  </div>
  <div class="description">
    description text about Flying Kittens! Inc.
  </div>
</div>
<div class="footer">
  <div class="copyright">&copy; 2016 Flying Kittenz! Inc.</div>
  <div class="social-icons">
    <div class="social-icon">
      FB
    </div>
    <div class="social-icon">
      TW
    </div>
    <div class="social-icon">
      YT
    </div>
  </div>
</div>
</body>
</html>
```

Notice how multiple elements can have the same class name. This makes it easy to target multiple related elements and give them the same styles. Let's do this by adding the following CSS to the `styles.css` file:

```css
body {
  /*
  The font-family property is _inherited_. This means that if we apply it to <body>, it will apply to all its children as well. This code sets the base font family for all the page. Because it's inherited, it can also be easily overridden with a simple CSS rule.
  */
  font-family: sans-serif;
}
/* This selects the top title element */
.title {
  padding: 0.5em; /* Add breathing space around the text. em are proportional to the current font size */
  color: #fff; /* color specifies the text color */
  background-color: #0099ff; /* background color will extend into the padding */
  margin-bottom: 0.5em; /* add breathing space below the element */
}

/*
The image and the description should go next to each other.
Let's give the image a width of 30% and the description 70%. That should take care of it.
*/
.image {
  width: 30%;
}
.description {
  width: 70%;
}

/*
All the text in the footer is centered. Since text-align is an inherited property,
we can add it to the element with class footer and it will apply to all its children
as well, centering the text everywhere inside
*/
.footer {
  text-align: center;
}
```

Even after doing all this, the result looks nothing like the design:

![Design without layout](https://s11.postimg.org/8fkdg717n/Screen_Shot_2016_10_31_at_08_06_19.png)

The one thing that could make our web page look more like the design would be to be able to layout elements horizontally. It looks like giving the image div a width of 30% and the description a width of 70% did not help place these elements next to each other. Indeed, the default display mode for `<div>` is block, which means that displaying a `<div>` in the flow will always generate a line break by default.

In the past, many techniques have been used to layout elements in horizontal rows rather than one on top of each other. The technique we will be looking at here is the modern Flexbox. Flexbox is part of the CSS3 specification, and lets us control our layout more powerfully with some CSS properties.

Let's add the following to our `styles.css` document:

```css
/*
Adding a display flex to a parent element will make all its children act like flexible boxes.
One of the things that this does by default is layout the elements horizontally, which is exactly
what we wanted in this case. There's a lot more to flexbox than simply setting the flex property!
*/
.social-icons, .main-section {
  display: flex;
}

```

Now the design looks like this. At least the elements are layed out next to each other:

![Start of layout](https://s17.postimg.org/qhtbtx9n3/Screen_Shot_2016_10_31_at_08_11_57.png)

Note that the div with class name `image` has 30% width, but the image inside it is overflowing:

![overflowing image](https://s17.postimg.org/nmg8n25n3/Screen_Shot_2016_10_31_at_08_12_19.png)

Let's fix this by giving the image a `max-width` of `100%`, and add some spacing for the social icons. Also note that the social icons are not centered anymore: the `text-align: center` property of the parent only applies to text content. Now that the boxes for each social icons are flexed, they don't have enough space to center their content. That's what we want anyway. We will add the `justify-content: center` CSS property to their parent to make it center its flexbox children.

```css
/*
This is called a "utility class". We can apply it on any image to make it comply to the
width of its parent.
*/
.responsive-img {
  max-width: 100%;
}

/*
This is the second time we select the `social-icons` class. That's perfectly fine in CSS!
*/
.social-icons {
  justify-content: center;
}

/* This will create some space between each social icon */
.social-icon {
  margin: 0 0.3em; /* This sets the margin to 0 for top and bottom, and 0.3em for left and right.
}

```

Let's add some spacing between the image and the description, as well as below the whole image + description block. To do this, add a `padding-right` of `0.5em` to the `.image` div, and a `margin-bottom` of `0.5em` to the `.main-content` div. Starting to look pretty good:

![after some spacing](https://s11.postimg.org/ocirylzvn/Screen_Shot_2016_10_31_at_08_19_34.png)

Let's add the following style rules to make the social icons look more like the design. Here, we're using a popular flexbox trick to center content both horizontally and vertically inside its parent:

```css
.social-icon {
  margin: 0 0.3em;
  /* add the below styles to the social icons */
  background-color:  black;
  color: white;
  width: 36px;
  height: 36px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
}
```

Finally it looks like this:

![social icons styling](https://s18.postimg.org/4fkumzhah/Screen_Shot_2016_10_31_at_08_28_42.png)

Let's put the final touches on this design. We need to apply a larger font size and weight to the title, and make the social icons look like social icons. For the title, use the `font-size` property to find an appropriate font size, and the `font-weight` property to make the text bolder.

Finally, let's install the [Font Awesome icon font](http://fontawesome.io) on our page to allow us to have access to a [huge set of icons](http://fontawesome.io/icons/)

Add the following to the `<head>` of your page:

```html
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css">
```

Then, to display the social icons, replace the "FB", "TW" and "YT" text with the following:

```html
    <div class="social-icon">
        <i class="fa fa-facebook">
    </div>
    <div class="social-icon">
        <i class="fa fa-twitter">
    </div>
    <div class="social-icon">
        <i class="fa fa-youtube">
    </div>
```

Not bad, we now have a web page that looks quite close to the design:

![final webpage](https://s22.postimg.org/iepga599t/Screen_Shot_2016_10_31_at_08_36_17.png)

We can keep iterating on it with our customer and the designer. Add a bit of spacing, replace the content with the real one, tweak some font sizes, etc. This iterative process is at the root of building web pages, and is facilitated by the use of the Dev Tools of your browser.

Here's the final HTML and CSS for this tiny template:

```html
<!doctype html>
<html>
<head>
  <title>Flying Kittens! Inc.</title>
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css">
  <link rel="stylesheet" href="styles.css">
</head>
<body>
<div class="title">Flying Kittens! Inc.</div>
<div class="main-section">
  <div class="image">
    <img class="responsive-img" src="http://placekitten.com/g/401/401">
  </div>
  <div class="description">
    description text about Flying Kittens! Inc.
  </div>
</div>
<div class="footer">
  <div class="copyright">&copy; 2016 Flying Kittenz! Inc.</div>
  <div class="social-icons">
    <div class="social-icon">
      <i class="fa fa-facebook"></i>
    </div>
    <div class="social-icon">
      <i class="fa fa-twitter"></i>
    </div>
    <div class="social-icon">
      <i class="fa fa-youtube"></i>
    </div>
  </div>
</div>
</body>
</html>
```

```css
html {
  box-sizing: border-box;
}
*, *::before, *::after {
  box-sizing: inherit;
}

body {
  /*
  The font-family property is _inherited_. This means that if we apply it to <body>, it will apply to all its children as well. This code sets the base font family for all the page. Because it's inherited, it can also be easily overridden with a simple CSS rule.
  */
  font-family: sans-serif;
  background-color: #f6f6f6; /* super-light grey background, enough to not be completely white */
}
/* This selects the top title element */
.title {
  padding: 0.5em; /* Add breathing space around the text. em are proportional to the current font size */
  color: #fff; /* color specifies the text color */
  background-color: #0099ff; /* background color will extend into the padding */
  margin-bottom: 0.5em; /* add breathing space below the element */
}

/*
The image and the description should go next to each other.
Let's give the image a width of 30% and the description 70%. That should take care of it.
*/
.image {
  width: 30%;
  padding-right: 0.5em;
}
.description {
  width: 70%;
}

/*
All the text in the footer is centered. Since text-align is an inherited property,
we can add it to the element with class footer and it will apply to all its children
as well, centering the text everywhere inside
*/
.footer {
  text-align: center;
}

/*
Adding a display flex to a parent element will make all its children act like flexible boxes.
One of the things that this does by default is layout the elements horizontally, which is exactly
what we wanted in this case. There's a lot more to flexbox than simply setting the flex property!
*/
.social-icons, .main-section {
  display: flex;
}

.main-section {
  margin-bottom: 0.5em;
}

/*
This is called a "utility class". We can apply it on any image to make it comply to the
width of its parent.
*/
.responsive-img {
  max-width: 100%;
}

/*
This is the second time we select the `social-icons` class. That's perfectly fine in CSS!
*/
.social-icons {
  justify-content: center;
}

.social-icon {
  margin: 0 0.3em; /* This sets the margin to 0 for top and bottom, and 0.3em for left and right.*/
  background-color:  black;
  color: white;
  width: 36px;
  height: 36px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
}

```

## Divitis and its remedy: semantic HTML and CSS normalize
The HTML we wrote in the previous section is riddled with `<div>` tags. In HTML, the purpose of tags is mainly to convey the structure of a document and `<div>` does not convey much about structure. For example, our title at the top is actually a heading, one of the main titles of the page. HTML has a specific element for this, the `<h1>`.

Changing our `<div class="title">` to an `h1` will have some consequences on the appearance of the title. This is because each browser has **default styles** that it applies to some HTML elements. This is what makes `<a>` links blue and underlined by default.

Unfortunately, each browser has a different view of what the default styles should be. For this reason, developers have made an effort to create a base CSS file called "normalize.css". Normalize defines a basic set of styles that allows us to use HTML's **semantic elements** with consistency across all browsers.

Back in HTML 4, the only way to convey the structure -- table of contents or outline -- of a web page was to use the heading tags, `<h1>` up to `<h6>`. Each heading level creates a sub-section of our document.

With the advent of HTML 5, many new tags were added to help structure our documents, like `<section>`, `<aside>` and `<article>`. Remember that HTML tags should not be used for styling content, but simply to convey this structure.

In our Flying Kittens example above, the main title should be an `<h1>` instead of a `<div class="title">`. The bottom container should be a `<footer>` instead of a `<div class="footer">`. And the main section could be inside a tag of `<section class="main-section">` rather than a simple `<div>`. If we do this exercise well, **the only places where `<div>` should be used are for grouping elements for the purpose of styling**. In all other places, there should be a better element to use.

Read this [MDN article about sectioning elements](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Using_HTML_sections_and_outlines) and modify your HTML structure to use them. Then, add the [Normalize.css](https://necolas.github.io/normalize.css/) file as a `<link>` tag on your page to have a standard base set of styles across all browsers. Make sure that any `<link>` tags that are not your own CSS appear **before your own CSS** so that your CSS will be more specific with respect to the cascade.

Our final HTML looks like this:

```html
<!doctype html>
<html>
<head>
  <title>Flying Kittens! Inc.</title>
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css">
  <link rel="stylesheet" href="styles.css">
</head>
<body>
<header>
  <h1 class="title">Flying Kittens! Inc.</h1>
</header>
<section class="main-section">
  <!-- here we use a div to add some spacing to the right of the image -->
  <div class="image">
    <img class="responsive-img" src="http://placekitten.com/g/401/401">
  </div>
  <p class="description">
    description text about Flying Kittens! Inc.
  </p>
</section>
<footer class="footer">
  <p class="copyright">&copy; 2016 Flying Kittenz! Inc.</div>
  <ul class="social-icons">
    <li class="social-icon">
      <i class="fa fa-facebook"></i>
    </li>
    <li class="social-icon">
      <i class="fa fa-twitter"></i>
    </li>
    <li class="social-icon">
      <i class="fa fa-youtube"></i>
    </li>
  </div>
</footer>
</body>
</html>

```

## Recipe: Integrating a design
We've come a long way from our initial boxification. We now have a basic recipe to integrate a design on a web page:

1. Boxify the design: draw a set of boxes that represents the structure of the page
2. Identify the semantic elements as well as elements that have the same styles
3. Write the *skeleton* of the HTML, using either a `<div>` or appropriate semantic element where needed.
4. Write some CSS to get closer and closer to the design. Start with the layout, using Flexbox to lay things out horizontally. Then, add more specific styles as you go.
5. Iterate until the web page looks close to the design. This might require some re-boxification, or simply adding more styles and refreshing your browser to see the changes.
6. ∞: **Always have Dev Tools open when integrating a web page**

## Addon: CSS Recipes
Here are some CSS recipes you can use when you need to get something specific done. The list is by no means exhaustive.

### Horizontally centered box
Sometimes we want to have a boxed content centered horizontally, with the box being no larger than a certain amount of pixels. To do this, we can use a mix of `max-width` and `auto` margins:

```html
<div class="centered-box">
Lorem ipsum blabla Lorem ipsum blabla Lorem ipsum blabla Lorem ipsum blabla Lorem ipsum blabla Lorem ipsum blabla Lorem ipsum blabla Lorem ipsum blabla Lorem ipsum blabla Lorem ipsum blabla Lorem ipsum blabla Lorem ipsum blabla Lorem ipsum blabla
</div>
```

```css
.centered-box {
    max-width: 450px; /* width will be 100% of parent, UP TO 450px */
    margin: 0 auto; /* margin auto on the left and right sides centers the element */
    padding: 1em; /* generous spacing to allow for a border */
    border: 1px solid black;
}
```

### Horizontally centered text and/or images
To center text or images, we can simply add `text-align: center` to the parent element.

### Vertical centering with flexbox
A common theme is having a big "hero" section at the top of a page, with some text centered in the middle of that section. We can achieve this horizontal/vertical centering easily with flexbox. Here's an example:

```html
<div class="centered">
  The text inside this box is centered both horizontally and vertically!
</div>
```

```css
.centered {
    display: flex; /* allows for vertical centering among other things */
    justify-content: center; /* centers flex children horizontally */
    align-items: center; /* centers flex children vertically */
    height: 100vh; /* since content flows from top to bottom, vertical centering ONLY makes sense if we have a specific height on an element. 100vh is 100% of the height of the window, making this a full-screen div */
}
```

### Circular image
Creating a circular image is as easy as starting with a square image, and giving it a `border-radius: 50%` style. This will create a "rounded corners" image where the corners are 50% of the size of the sides, effectively making a circle!

### Image thumbnails
Creating an image that looks like a thumbnail is easy. Here is some basic CSS to get that done:

```css
.thumbnail {
    border: 1px solid #999;
    padding: 0.5em;
}
```

### Full-section backgrounds
To add a full-section background to a div (using the `100vh` trick from above), we can set a `background-image` on the element, and set the `background-size` property to `cover`. This means the background will stretch as much as needed to cover all the section.


# Integration practice
Use your own HTML and CSS, plus everything you learned to integrate the following three templates. Note that there are some effects you may not be able to achieve from the start. Remember to follow the recipe we gave you, and to go from most generic to most specific. Substitute placeholder images and text where necessary.

## Template 00
![template 00](https://s14.postimg.org/qenfuknwh/template_00.png)

## Template 01
![template 01](https://s14.postimg.org/qh7bherk1/template_01.png)

# Grid
The CSS grid layout module excels at dividing a page into major regions or defining the relationship in terms of size, position, and layer, between parts of a control built from HTML primitives.

Like tables, grid layout enables an author to align elements into columns and rows. However, many more layouts are either possible or easier with CSS grid than they were with tables. For example, a grid container's child elements could position themselves so they actually overlap and layer, similar to CSS positioned elements.
The example below shows a three-column track grid with new rows created at a minimum of 100 pixels and a maximum of auto. Items have been placed onto the grid using line-based placement.
### HTML
<div class="wrapper">
  <div class="one">One</div>
  <div class="two">Two</div>
  <div class="three">Three</div>
  <div class="four">Four</div>
  <div class="five">Five</div>
  <div class="six">Six</div>
</div>

### CSS
.wrapper {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px;
  grid-auto-rows: minmax(100px, auto);
}
.one {
  grid-column: 1 / 3;
  grid-row: 1;
}
.two {
  grid-column: 2 / 4;
  grid-row: 1 / 3;
}
.three {
  grid-column: 1;
  grid-row: 2 / 5;
}
.four {
  grid-column: 3;
  grid-row: 3;
}
.five {
  grid-column: 2;
  grid-row: 4;
}
.six {
  grid-column: 3;
  grid-row: 4;
}

### Output



## Template 02
![template 02](https://s14.postimg.org/xvwn9sdfl/template_02.png)
