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

In terms of other ways to style text, we have the following `text-justify` which makes the edges of the text be glued to the edges of the web page. There is also the following command `text-XX-POS` where `XX` can take values `sm, md, lg, xl` and can mean any of the horizontal positions in pixels and where `POS`can take values either `left, center, right`. You can also have this command which helps to align elements vertically/hoizontally `align-SID`, and `SID` can take values : `baseline, top, middle, bottom, text-bottom, text-top, right`.
