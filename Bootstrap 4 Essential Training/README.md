# Bootstrap 4 Essential Training

We need to use a content delivery network or CDN. This mechanism saves the bootstrap in the cache. This allows offine development. To install there are 4 different ways : to download the pre compiled Bootstrap CSS and JS files, or you can use a boostrap CDN, or download all the source files needed to create the boostrap or you can use a package manager like NPM, Composer or NuGet. Typicically in our project we mostly use the following files : bootstrap.min.css and bootstrap.min.js . In the index.html file you want to paste the following code :

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible content="IE-edge">
  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
  <meta http-equiv="x-ua-compatible" content="ie-edge">
  <link rel="stylesheet" href="css/bootstrap.min.css">
  <title>Bootstrap</title>
</head> 
<body>
<div class="container">
</div>

<script src="js/jquery.slim.min.js"></script>
<script src="js/popper.min.js"></script>
<script src=*js/bootstrap.min.js"></script>
</body>
</html>
```

Reboot makes styles consistent across different browsers and platforms. Bootstrap uses rems as a unit of measurement. It controls the size of the fonts across the entire platform. The margin-top is avoided, so as to use only the bottom margin when possible. We will also need to use the inherit property whenever possible. Border-box sizin doesn't add extra padding where it would be added normally. Native font stacks are used, they are native relative to the browser, the OS. 

If you need text that is bigger in size than the headers h1 you may use divs with the following classes : `display-1, display-2,..., display-5`. When you specify that a paragraph has the `lead` style then this paragraph become bold, and is bigger in font-size. It therefore starts to look like a lead paragraph.

In terms of other ways to style text, we have the following `text-justify` which makes the edges of the text be glued to the edges of the web page. There is also the following command `text-XX-POS` where `XX` can take values `sm, md, lg, xl` and can mean any of the horizontal positions in pixels and where `POS`can take values either `left, center, right`. You can also have this command which helps to align elements on a line `align-SID`, and `SIDE` can take values : `baseline, top, middle, bottom, text-bottom, text-top, right`. In a similar manner you may also format the capitalization of text by using the following command : `text-TYPE` where `TYPE` can be either of `lowercase, uppercase, capitalize, monospace`. In a similar way you can style the text as : `font-STYLE` where `STYLE` can be any of the following : `italic, weight-normal, weight-light, weight-lighter, weight-bold, weight-bolder`. There are also text modifiers : `text-decoration-none` for example removes the underline of a link, `text-rest` makes the color of a link the same color as the background. You can also have the following command `text-FLOW` where `FLOW` can be either `wrap, nowrap, break, truncate`. This prevents long strings of text from breaking the layout. 

There are various keywords you can use to style HTML elements. For example the `list-unstyled` keywords used in order to remove the bullets in a list. Also if you want to put a list on one line for example you could write : `list-inline` on a UL, and `list-inline-item` on each LI associated to the UL. You can also add text that looks like a block quote, you do this by adding the element : `<blockquote class="blockquote"></blockquote>`. A blockquote can also have a blockquote footer. The whole code is below :

```
<blockquote class="blockquote">
This is a quote.
</blockquote>
<div class="blockquote-footer">
Jane
</div>
</blockquote>
```
It is also possible to make the quote align on the right by writing as a class name : `<blockquote class="blockquote blockquote-reverse">`. Then there is the `text-COLOR` where color can be any of : `primary, secondary, success, danger, warning, info, light, dark, body, black-50, white-50, muted, white`, and we can set the background color with `bg-COLOR` where COLOR in this case can by any of the following : `primary, secondary, success, danger, warning, info, light, dark, white, transparent`. 

There are also classes that you can use for images, such as `img-fluid`. This makes images responsive to the container, so they adjust  to the width of the container. You can also make thumbnail images by writing `img-thumbnail`. You can also set the style of the rounded image as : `ROUNDED(-SID) (-SHA) (-SIZ)`, where `SID` can be top, right, bottom, left, `SHA` can be circle, pill and `SIZ` can be 0, sm, lg. You can also align images with `float-left, float-right`. To align text `text-center`. And we centered the blcok image by writing `mx-auto`. An example of a figure is as follows :

```
<figure>
  <img class="img-fluid rounded-circle" src="images/testimonial-janeh.jpg" alt="Photo">
  <figcaption></figcaption>
</figure>  
```
It is also possible to add a radius to the border radius instead: `<img class="img-fluid figure-img" style="border-radius:20px"></img>`. There are color variables as follows : `--blue, --indigo, --purple, --pink, --red, --orange, --yellow, --green, --teal, --cyan, --white, --gray, --gray-dark, --light, --dark, --primary, --secondary, --success, --info, --warning, --danger`. You can also add breakpoints as follows : `--breakpoint-xs, --breakpoint-sm, --breakpoint-md, --breakpoint-lg, --breakpoint-xl`. It is also possible to change the font-family as follows : `font-family-sans-serif, font-family-monospace`. To use the above colors you need to define a variable as follows :

`<h2 style="color: var(--yellow);">Testimonials</h2>`

Imagine you want to define your own CSS variale then you must right `:root` as follows below. Here we redefine the default value of the color of the --pink variable.

```
<style>
  :root {
    --pink : #C4226F;
  }
</style>

<h2 style="color : var(--pink);"> Testimonials </h2>
```
Containers have either a responsive fixed width that snap to certain breakpoints or you can have fluid containers that take up 100% of the width of the view port. Bootstrap uses a 12-clumn grid system. To use this we are going to have to work with the container, the row and the column classes. To create a container you need to add a div and add a class of `container(-SIZ)` where `SIZ` can be any of `sm, md, lg, xl, fluid`. Essentially the endings except for `fluid` allow you to resize the container so that it remains at a fixed width despite the size of the screen. To make an image cover half the height of the screen you can write :

```
<header style="height:50vh background: url(images/background.jpg) no-repeat center center; background-size: cover;margin-bottom: 20 px">
  <img src="images/wisdompetlogo.svg" alt="Widsom Pet Logo">
</header>
```
When you use the container fluid, the div never snaps to a certain size and always fills maximally the screen. You can use the columns and rows features as follows :

```
<section id="services">
  <div class="container">
    <div class="row">
      <article class="col">
      ...
      </article>
       <article class="col">
      ...
      </article>
       <article class="col">
      ...
      </article>
    </div>
  </div>
</section>
```
We can also use this command : `row-cols(-BP)(-COL)`. Where `BP` can be any of `sm, md, lg, xl`, and `COL` can be any number from 1 to 6. The command `no-gutters` removes the 30px padding between the columns. As for the columns you can have the following command : `col(-BP)(-COL)` where `BP` can be any of `sm, md, lg, xl`, and `COL` can be any number between 1 and 12. You can align columns vertically by writing `align-TYP-DIR` where `TYP` can be items or self, and `DIR` can be start, center or end. Similarly you can align columns horizontally by writing : `justify-contente-DIR` and `DIR` can be any of start, center, end, around, between.

For example when you type `row-cols-3` it will fit 3 articles on each row. If you write `row-cols-lg-4` then when the screen is large, there will be four articles which will fit onto the screen. Suppose you specify two sections `<section class="col-3>` and `<section class="col-6">` then the second section will take up twice the space horizontally than the first section. You can write for example :

```
<div class="container" id="services">
  <div class="row align-items-center justify-content-center">
    <section class="col-3">
    </section>
    <section class="col-3">
    </section>
    <section class="col-3">
    </section>
  </div>
</div>
```
