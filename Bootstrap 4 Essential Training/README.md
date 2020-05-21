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
