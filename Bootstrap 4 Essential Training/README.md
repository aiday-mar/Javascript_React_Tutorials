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

Imagine you want one article per page when the screen is extra small and otherwise you want two articles on one row, and when the screen is middle size you can have three articles :

```
<div class="container" id="services">
  <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3">
    <section class="col">
    </section>
    ...
  </div>
</div>
```
Another way of writing this is by writing as below. Here each section takes up half of the horizontal space.

```
<div class="container" id="services">
  <div class="row">
    <section class="col-6">
    </section>
    ...
  </div>
</div>
```
A more refined version is : `<section class="col-sm-6 col-md-4 col-lg-3 col-xl-2">`. You can also offset elements by writing the following : `offset-BP-COL` where BP is one od the breakpoints and the COL can take any values between 1 and 11. An example of the use is : `<section class="col-sm-4 offset-sm-2">`. You can also nest columns one in the other, you do this by placing a row inside an existing column. For example:

```
<div class="container" id="services">
  <div class="row">
    <section class="col-sm-8">
    </section>
    <section class="col-sm-4">
      <div class="row">
        <div class="col-sm-4">
        </div>
        ...
      </div>
    </section>
  </div>
</div>
```
You can change the order to sections by typing in the class for example : `<section class="col order-2">`. When you specify an order on a line better to specify the order of all the elements on that row. When you type `class="d-flex flex-column"` then the elements appear side by side. You can vertically align elements as follows, either use they keyword : `align-items-ALN` or `align-self-ALN` where ALN is any of `start, center, end`. If you want to move elements horizontally you can write : `justify-content-ALN` where ALN can take values in `start, end, center, around`. The `around` keyword tries to put equidistant space between each column. 

There are other ways to control the position of elements, aside from using the grid. You can specify the position classes as `fixed-top, fixed-bottom, sticky-top`. The sticky-top makes the element stick to the top of the page even when there is scrolling. You can also use the display tag as follows `d(-BP)-TYP` where BP can be any of `sm, md, lg, xl`, and TYP can be any of `none, inline, inline-block, block, table, table-row, table-cell, flex, inline-flex`. By default flex elements are block-level elements. You can also write : `d(-BP)(-inline)-flex`. When you write just `d-inline` you loose the ability to display elements of a specific size, when you write `d-inline-block` here you have the elements inlined and they are of the size that you specified. You can also make this as :

```
<div class="bg-info d-sm-inline-flex">
  <div class="item">Item 1</div>
  ...
</div>
```
You can specify the direction as : `flex(-BP)(-DIR)(-reverse)`, and `DIR` can either be `row, column`, similarly we have `flex(-BP)-WRP(-reverse)` where `WRP` can be either `wrap, nowrap`. We can stack elements in a column as : `<div class="d-flex flex-sm-column">...</div>`. If you want to align all the elements together on the left we have : `<div class="d-flex flex-wrap align-content-start">...</div>`. Another way of writing is :

```
<div class="clearfix">
  <div class="item float-sm-left">Item 1</div>
  ...
</div>
```

You can add spacing as follows : `p(SID)-BP-(N)SIZ`. where SID can be `t,r,b,l,x,y`, and SIZ can be any of 0 to 5 or auto, for the padding. When this concerns the margin we have `m(SID)-BP-(N)SIZ`. The N means a negative value. 

You can also change the visibility of the elements by using either the `visible` or `invisible` classes. You can also write `class="d-sm-none"`. You can also have different sizing of elements as follows : `SIZ(-AMT)` where `SIZ` can be `w,h,mw,mh,vw,vh,min-vw, min-vh` and `AMT` can be `25, 50, 75, 100, auto`. Where vw is viewport width and vh is viewport height, w just means width of the parent and h means height of the parent. You can specify the border as follows : `BORDER(-SID)(-COL)(-SIZ)` where `SID` takes values in `top, right bottom, left`, `COL` takes values in `primary, secondary, success, danger, warning, info, light, dark, white` and `SIZ` can be any of `0, sm, lg`. For example:

```
<style>
  .item {
    width : 150px;
    height : 150px;
    display : inline-block;
    margin : 10px;
    background : #f5f5f5;
    border : 3px solid yellowgreen;
  }
</style>

<div class="container">
  <div class="item border border-primary"></div>
  <div class="item border-0 "></div>
</div>
``` 

Another important component aside from the grid are the navigation components : the navs, the tabs, pills and navbars. The classes related are : `nav, nav-item, nav-link, active, disabled, nav-pills, nav-tabs, nav-fill, nav-justified, flex-column`. An example is :

```
<nav class="nav nav-tabs justify-content-center">
  <a class="nav-item nav-link active">Link 1</a>
  ...
</nav>
```
Instead of `nav-tabs` you can write `nav-pills`. Instead of writing `justify-content-center` you can write `nav-justified` or `nav-fill` or `flex-column` or `flex-sm-row`. We can control when the navbar will expand by typing : `navbar-expand(-BP)` where `BP` can be any of `sm, md, lg, xl`. You can specify some colors of the navbbar using `bg-COLOR`, `navbar-light`, `navbar-dark`. An example is :

```
<nav class="navbar bg-light navbar-light navbar-expand-sm"
style="background-color: red">
  <a class="navbar-brand d-none d-sm-inline-block" href="#">
    <img src="images/brandlogo.svg" style="width:80px" alt="Logo">
  </a>
  <div class="container">
    <div class="navbar-nav ml-sm-auto">
      <a class="nav-item nav-link" href="#">Home</a>
      ...
    </div>
    <span class="navbar-text d-none d-xl-inline-block"> Some navbar text </span>
 </div>
</nav>
```

We have also the navbar options `navbar-brand` and `navbar-text`. We are going to add a dropdown to the navigation. A dropdown requires a container to work. We have the following dropdown keywords : `dropdown, dropdown-toggle, data-toggle="dropdown"`. We also have the following keywords that can be used `dropdown-menu, dropdown-item`.

```
<div class="dropdown">
  
  <a class="nav-item nav-link dropdown-toggle"
     data-toggle="dropdown" id="servicesDropdown"
     aria-haspopup="true" aria-expanded="false"
     href="#services"> Services </a>
  
  <div class="dropdown-menu" aria-labelledby="servicesDropdown">
    <a class="dropdown-item" href="#"> Item 1 </a>
    ...
  </div>
</div>
```
You can have forms in web pages. The keywords used are : `form-inline, form-control`. An example is :

```
<form class="form-inline">
  <input class="form-control mr-2" type="text" placeholder="Search">
  <button class="btn btn-outline-light" type="submit">Go</button>
</form>
```

You can also create collapsible content, for that we will need keywords such as `collapse, navbar-collapse, id`. There are various classes that may be used like `navbar-toggler, navbar-toggler-icon`.

```
<button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#myTogglerNav" 
aria-controls="myTogglerNav" aria-expanded="false" aria-label="Toggle navigation">
<span class="navbar-toggler-icon"></span>
</button>

<div class=*collapse navbar-collapse" id="myTogglerNav">
  <div class="navbar-nav">
  ...
  </div>
</div>
```

You can also create a button in bootstrap using the `btn` class, where you can specify the button size with `btn-SIZ` and `SIZ` can be any of `sm, lg`. In a similar way you may specify the color of the button as follows `btn-COLOR`, and you can also define the outline as follows `btn-outline-COLOR`. The `btn-block` can be used so that the button occupies the entire width of the container. It doesn't matter whether the HTML tag is a link, a button or an input, the tag still looks like a button when you append the right class.

To group buttons together you can use the `btn-group` class. There is also a vertical version option for button groups `btn-group-vertical`. There is also a class called `basges` that can be used in conjunction with `badge-pill` and `badge-COLOR`. An example of the use is :

```
<span class="badge badge-danger badge-pill"> This is a badge </span>
```
You can also create a progress bar using the `progress` container, which you use with the `progress-bar` item. You can also make a striped bar using `progress-bar-striped`. This progress bar can be animated with `progress-bar-animated`. You can also assign the role of the progressbar with `role="progressbar"` and you can use the keyword `aria-valuenow`, `aria-valuemin` which holds the minimum value and `aria-valuemax` which holds the maximal value. This can be coded as follows :

```
<div class="progress">
  <div class="progress-bar bg-success progress-bar-striped progress-bar-animated" role="progressbar" style="width:73%; height: 40px;">73%</div>
</div>
```
 
The above gives a bar which is 73% of the container, and the text "73%" appears too in the progress bar. You can even add progress bars one on top of each other as follows :

```
<div class="progress">
  <div class="progress-bar bg-info" style="width:15%"></div>
  <div class="progress-bar bw-warning" style="width:30%"></div>
</div>
```
We have list groups which can be specified with the `list-group` containers, `list-group-item` items, and the `list-group-item-COLOR` property and the `list-group-horizontal(-BP)`. An example is :

```
<ul class="list-group mb-3">
  <li class="list-group-item lit-group-item-action">Item 1</li>
  ...
</ul>
```
You cana also use `breadcrumb`s in the navigation along with `breadcrumb-item`. An example is as follows :

```
<style>
  .breadcrumb-item+.breadcrumb-item::before {
    content: '|'
  }
</style>

<nav class="breadcrumb">
  <a class="breadcrumb-item" href="#">Home</a>
  <span class="breadcrumb-item active">Nutrition</span>
</nav>
```
The style element above changes the separator between the breadcrumb items, where the + means we are changing the style for the elements after the first element. You can also add shadow classes using the following keywords : `shadow-none, shadow-sm, shadow, shadow-lg`. An example is as follows :

```
<section class="border my-4 p-3 shadow">
  <h4>Header</h4>
  <div> Some text </div>
</section>
```
The jumobotron is a component for a highlighted piece of content and it is commonly used at the top of many websites. For that you need to use the `jumbotron` container and the `jumbotron-fluid` items. We have the following code : 

```
<header class="jumbotron jumbotron-fluid mt-4">
  <div class="container">
    <div class="display-2 mb-4"> Our mission </div>
    <p class="lead"> The paragraph </p>
  </div>
</header>
```

There is the `table` class that can be used to create tables, along with `table-dark`, `table-striped`, `table-bordered`, `table-borderless`, `table-hover`. You can change the color of the table header by writing : `thead-light`, `thead-dark`. You can also write `table-COLOR` for the color of the border and use `bg-color` for the color of the background of the cell. You can size the tables a follows with `table-sm, table-responsive(-BP)`. An example is as follows :

```
<table class="table table-hover table-responsive">
  <thead><tr><th scope="col">header 1</th>...</tr></thead>
  <tbody>
    <tr><th scope="row"> 1 </th> ...
  </tbody>
</table>
```

You can also make card looking views using the following classes `card, card-body, card-text, card-title, card-subtitle, card-link, card-img`. You can also assign specific colors such as `bg-COLOR, border-COLOR, text-COLOR`. An example is :

```
<div class="container">
  <section class="card mb-5">
    <div class="card-body">
      <img class="card-img img-fluid" src="some-link">
      <h2 class="card-title">Title</h2>
      <h5 class="card-subtitle">Subtitle</h5>
      <p class="card-text">The text</p>
    </div>
    <div class="list-group list-group-flush">
      <a class="list-group-item" href="#">About</a>
      ...
    </div>
  </section>
</div>
```
You can also group the cards as follows `car-group`. You can create decks using `card-deck`:

```
<div class="container">
  <div class="card-group">
    <section class="card mb-5">
    </section>
    ...
  </div>
</div>
```

When you instead use `card-columns` the cards are in one column and the top of a card is aligned to the bottom of the one above. Or you can use the grid as follows :

```
<div class="container">
  <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3 row-cols-lg-4">
    <div class="col">
      <section class="card mb-5"></section>
    </div>
    ...
  </div>
</div>
```
An example of the use of the `media` class is :

```
<section class="media mb-4">
  <img class="d-flex align-self-center mr-3 img-fluid rounded w-25" src="#">
  <div class="media-body">
    <h2>Header</h2>
    <p>Text<p>
  </div
</section>
```
You can also use forms with `form-group` and `form-text`, `form-control`, `form-control-label`, `form-control-file`, `form-check`, `form-check-label`, `form-check-input`, `form-check-inline`.

```
<form>
  <fieldset class="form-group">
    <legend>Pet Info</legend>
    <div class="form-group">
      <label class="form-control-label" for="ownername">Owner name</label>
      <input class="form-control" type="text" id="ownername" placeholder="Your name">
    </div>
  </fieldset>
</form>
```

There is also similar code for the case when we have checkboxes.

```
<div class="form-check form-check-inline">
  <label class="form-check-label">
    <input class="form-check-input" type="checkbox">Option 1</input>
  </label>
</div>
...
```

You can also change the sizes of the forms with `form-control-sm` and `form-control-lg`. We can also use the keywords `has-COLOR` and `form-control-COLOR`. An example is :

```
<div class="form-group has-success form-inline">
  <label class="form-control-label" for="owneremail">Email</label>
  <input class="form-control mx-sm-2 form-control-success" type"email">Your email</input>
  <small class="form-text text-muted" id="emailHelp">We'll never share your email</small>
</div>
```
There are classes that you can use such as `form-row` and `col-auto`, `col-form-label`.

```
<div class="form-group row">
  <label class="col-form-label text-md-right col-md-2" for="ownername">Owner</label>
  <div class="col-md-10">
    <input class="form-control" type="text" id="ownername" placeholder"Your name">
  </div>
</div>
```
As well as :

```
<div class="form-group row">
  <div class="offset-md-2 col-auto">
    <button class="btn btn-primary" type="submit">Submit</button>
  </div>
</div>
```

You can create input elements using the following classes `input-group, input-group-prepend, input-group-append, input-group-text, aria-label, sr-only`. We have an example below :

```
<div class="form-group">
  <label class="form-control-label" for="donationamt">Donation amount</label>
  <div class="input-group">
    <div class="input-group-prepend">
      <div class="input-group-text">
        <input type="checkbox" id="confirm-donation" checked aria-label="checkbox for confirming donation">
      </div>
      <div class="input-group-text">$</div>
    </div>
    <input type="text" class="form-control" id="donationamt" placeholder="Amount">
  </div>
</div>
```
You can have custom controls `custom-TYP` where `TYP` can be any of `select(-sm)(-lg), radio, checkbox, switch, range, file-input`. Or we can use the following classes `custom-control-label, custom-control, custom-control-input`. An example is :

```
<div class="custom-control custom-checkbox">
  <input class="custom-control-input" type="checkbox" id="input1">
  <label class="custom-control-label" for="input1">Input 1</label>-
</div>
```
You can also have `custom-switch` instead of `custom-checkbox`. Here you can also have a range as follows :

```
<div class="form-group">
  <label for="happinesslevel">Level of happiness</label>
  <input type="range" class="custom-range" min="0" max="10" id="happinesslevel">
</div>
```
You can also make a tab for uploading files as follows :

```
<div class="form-group">
  <div class="custom-file">
    <input type="file" class="custom-file-input" id="petphoto">
    <label class="custom-file-label" for="petphoto">Upload photo</label>
  </div>
</div>
```

Tooltips are used by writing for example `data-toggle="tooltip"`. Tooltips can be configured with a data attribute or with JavaScript. You can activate the tooltip with JavaScript as follows :

```
$(function () {
  $('[data-toggle = "tooltip" ]').tooltip({ OPTIONS })
});
```

The HTML would be as follows :

```
<div class="tooltip bs-tooltip-top" role="tooltip">
  <div class="arrow"></div>
  <div class="tooltip-inner">
    Some tooltip text !
  </div>
</div>
```
Where we can use `placement, trigger, html`. Example : `<a href="#" data-toggle="tooltip" data-placement="top" data-html="true">`. You can also use pop overs a follows : `data-toggle="popover", title="text", data-content="content"`. In a similar way you activate this using jQuery :

```
<button type="button" class="btn btn-info" data-toggle="popover" title="Checkups" data-trigger="hover"
data-content="Our standard checkups offer many services"> Checkup Info </button>

$(function () {
  $('[data-toggle="popover"]').popover({
    placement : "top"
  })
})
```
You can create alerts as follows using the keywords : `alert, alert-COLOR, alert-heading, alert-link, alert-dismissible, fade, show`. An example is as follows :

```
<div class="alert alert-info alert-dismissible fade show"> 
  <button type="button" class="close" data-dismiss="alert">
  <span aria-hidden="true">&times;</span>
</div>
```

We also have a dropdown class for which we can use the following keywords : `dropdown, dropdown-toggle, dropdown-menu, dropdown-item, dropdown-header, dropdown-divider, disabled, dropup, dropdown-menu-right, dropdown-toggle-split`. An example is :

```
<div class="dropdown">
  <button class="btn btn-primary dropdown-toggle" type="button"
  id="dropdownMenuButton" data-toggle="dropdown" aria-haspopup="true"
  aria-expanded="false">
  Services
  </button>
  
  <div class="dropdown-menu" aria-labelledby="dropdownMenuButton">
    <div class="dropdown-header">Serice options</div>
    <a class="dropdown-item" href="#">Option 1</a>
    <div class="dropdown-divider"></div>
    <a class="dropdown-item" href="#">Other</a>
  </div>
</div>
```
We can also make the toggle button and the button with the text separate as follows : 

```
<button type="button" class="btn btn-primary">Sercices</button>
<button class="btn btn-primary dropdown-toggle" type="button"
id="dropdownMenuButton" data-toggle="dropdown"
aria-haspop="true" aria-expanded="false">
<span class="sr-only">Toggle Dropdown</span>
</button>
```
We can also use collapse and accordion elements. Accordions are groups of collapses. To set up a collapse, you create a link or a button that activates the collapse element. You can also add a `data-toggle="collapse"` and the ID or the `data-target`. Accordions require a container, it should contain the `show` class and the `dropdown-menu` class, and the `card` class. We include below an example of a set of cards that are collapsible.

```
<div id="servicesaccordion" role="tablist" aria-multiselectable="true">
  
  <div class="card">
    <div class="card-header" role="tab" id="groomingheading">
      <h5 class="mb-0">
        <a data-toggle="collapse" data-parent="servicesaccordion" 
        href="#grooming" aria-expanded="true" aria-controls="grooming">Grooming</a>
      </h5>
    </div>
    
    <div id="grooming" class="collapse show" role="tabpanel" aria-labbeledby="groomingheading">
      <div class="card-block">
        <p> Some collapsible text </p>
      </div>
    </div>
  </div>
</div>
```

Modals show up as an overlay on the top of the page. Modals use a button or a link, along with an ID or a `data-target` class, as well as the `data-toggle="modal"` class. We should also use the `modal` class. The `modal-dialog` is used to create additional spacing, and you can use the `modal-content` for the main content of the modal. You can also use the `modal-header`, and the `modal-body` is where you put the main content. There is also an optional footer `modal-footer`. There are other options like `modal-title`, `modal-dialog-centered`, `modal-dialog-scrollable`, `data-dismiss="modal"`. An example is :

```
<button type="button" class="btn btn-primary mt-4" data-toggle="modal" data-target="#servicesmodal">More Info</button>

<div class="modal fade" id="servicesmodal">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title">Pest control</h5>
        <button type="button" class="close"
        data-dismiss="modal" aria-label="close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">
        <p> Some test </p>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-dismiss="modal">Back</button>
    </div>
  </div>
</div>
```
To set up a carousel you create a container div and give it a class of carousel. You can use the following classes `carousel, slide, carousel-fade, carousel-inner, carousel-item, active, d-blocl, w-100, carousel-caption, ride, interval, pause, touch, keyboard, wrap, carousel-control-(prev)(next), carousel-control-(prev)(next)-icon, carousel-indicators, data-target="target", data-slide-to="#", `. An example is :

```
<div class="carousel slide carousel-fade" id="featured" data-ride="carousel">
  <ol class="carousel-indicators">
    <li data-target="#featured" data-slide-to="0"></li>
    <li data-target="#featured" data-slide-to="1"></li>
    <li data-target="#featured" data-slide-to="2"></li>
  </ol>
  <div class="carousel-inner">    
    <div class="carousel-item">
      <img class="d-block w-100" src="images/carousel-lifestyle.jpg" alt="lifestyle">
    </div>
    <div class="carousel-item">
      <img class="d-block w-100" src="images/carousel-fish-jpg" alt="Mission">
      <div class="carousel-caption d-none d-mb-block">
        <h3>Some header</h3>
        <p> Some paragraph</p>
      </div>
    </div>
    <div item="carousel-item active">
      <img class="d-block w-100" src="images/carousel-vacations.jpg" alt="lifestyle">  
    </div>
  </div>
  
  <a class=*carousel-control-prev" href="#featured" role="button" data-slide"prev">
    <span class="carousel-control-prev-icon" aria-hidden="true">
      <span class="sr-only">Previous</span>
    </span>
  </a>
  <a class="carousel-control-next" href="#featured" role="button" data-slide="next">
    <span class="carousel-control-next-icon" aria-hidden="true">
      <span class="sr-only">Next</span>
    </span>
  </a>
</div>
```

Scrollspy is a component that allows you to keep track of the scroll of the page. The main data-atttributes are : `data-spy="scroll", position: relative, data-target="ID", fixed-top, data-offset`. We have an example below of the menu bar with the scrolling effect :

```
<body data-spy="scroll" data-target="#navbar-site" data-offset="80">
  
  <nav id="navbar-site" class="navbar navbar-dark bg-dark navbar-expand-sm fixed-top">
    <div class="container">
      <ul class="navbar-nav">
        <li class="nav-item"><a class="nav-link" href="#mission">Mission</a></li>
        ...
      </ul>
    </div>
  </nav>
  
</body>

<script>
  $(function() {
    var topoffset = 70;
    
    $('.navbar-nav a').click(function () {
      if (location.pathname.replace(/^\//, '') ===
      this.pathname.replace(/^\//, '') &&
      location.hostname === this.hostname) {
        var target = $(this.hash);
        target = target.length ? target : $('[name=' + this.hash.slice(1) + ']');
        if (target.length) {
          $('html, body').animate({
            scrollTop : target.offset().top-topoffset
          }, 500);
          return false;
        }
      }
    });
  });
</script>
```

Toasts are notifcations that can appea on the site. For this you use the following styles `toast, toast-header, toast-body, animation, autohide, delay,`. We do the setup for the toast as follows : `data-dismiss="toast"`. An example is :

```
<div class="toast" role="alert" aria-live="assertive" aria-atomic="true" data-delay="5000" style="position:absolute; top: 1rem; right: 1rem;">
  <div class="toast-header">
    <strong class="mr-auto">About</strong>
    <button type="button" class="close" data-dismiss="toast" aria-label="Close">
      <span aria-hidden="true">&times;</span>
    </button>
  </div>
  <div class="toast-body">
    The content
  </div>
</div>

<button id="showToast" class="btn btn-primary mx-auto">About</button>

<script>
  $(document).ready(function() {
    $("#showToast").click(function() {
      $('.toast').toast('show');
    });
  });
</script>
```
You can also create spinners using the `spinner, spinner-TYP(-SIZ)` classes, where `TYP` can be any of `border, grow`, and you can also use `text-COL`.

```
<button id="showToast" class="btn btn-primary mx-auto">
  <span id="mySpinner" class="d-none">
    <span class="spinner-border spinner-grow-sm text-light" role="status" aria-hidden="true"></span>
    <span class="sr-only">Loading...</span>
  </span>
About</button>

<script>
  $(document).ready(function() {
    $("#showToast").click(function() {
      $('.toast').toast('show');
      
      $('#myToast').on('shown.bs.toast', function() {
        $('#mySpinner').removeClass('d-none');
      });
      
      $('#myToast').on('hidden.bs.toast', function() {
        $('#mySpinner').addClass('d-none');
      });
    });
  });
</script>
```

We can edit the pagination as follows. We need the classes `pagination, page-item, active, disabled, page-link`. We have the following code that also draws arrows on either side of the list :

```
<nav class="mt-5" aria-label="page navigation">
  <ul class="pagination justify-content-center">
    <li class="page-item"><a class="page-link" href="#"> < </a></li>
    ...
    <li class="page-item"><a class="page-link" href="#"> > </a></li>
  </ul>
</nav>
```

Stretched links can be implemented with the following class `stretched-link`. An example is :

```
<div class="card">
  <div class="card-body">
    <h2 class="card-title"> Our mission </h2>
    <p class="card-text"> Some text </p>
    <a href="#" class="btn btn-primary stretched-link">More info</a>
  </div>
</div>
```
You can also embed pieces of code from other websites. For this you can use the following classes `embed-responsive, embed-responsive-SIZ, embed-responsive-item`. For example:

```
<div class="embed-responsive embed-responsive-16by9">
  <iframe class="embed-responsive-item" width="560" height="315" src="youtube video link">
</div>
```
