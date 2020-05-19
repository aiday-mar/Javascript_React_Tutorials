# Javascript : Modern Browser APIs

Here you may find the notes from the following Linked In course : https://www.linkedin.com/learning/javascript-modern-browser-apis/building-apps-with-modern-javascript . 

There is an API called request animation frame that allows you to sync up the display of the refresh cycle.

```
<canvas width="400" height="400" id="canvas1">
  Your browser does not support the Canvas element
</canvas>
<button id = "btnStop">Stop Animation</button>
...

<script>
  window.addEventListener("load", init);

  document.getElementById("btnStop").addEventListener("click", function(){
    cancelAnimationFrame(animationRef);
  })

  cvs = document.querySelector("#canvas1");
  ctx = cvs.getContext("2d");

  var rectX = 0;
  var rectY = 200;
  var rectW = 40;
  var canvas = context = null;
  var animationRef = null;

  function init() {
    canvas = document.getElementById('canvas1');
    context = canvas.getContext("2d");

    blank(context);

    animationRef = requestAnimationFrame(anim);
  }

  function blank(theContext) {
    theContext.fillStyle = "#00ddee";
    theContext.fillRect(0, 0, theContext.canvas.width, theContext.canvas)
  }

  function anim(timestamp) {
    if (rectDir > 0 && (rectX + rectW) < context.canvas.width) {
      if((rectX + rectW + rectDir) >= context.canvas.width){
        rectDir = -rectDir;
      }
      else {
        rectX += rectDir;
      }
    }
    else if (rectDir < 0 && rectX >= 0) {
      rectX += rectDir;
      if (rectX < 0) {
        rectDir = -rectDir;
      }
    }

    blank(context);
    context.fillStyle = "yellow";
    context.strokeStyle = "red";
    context.lineWidth = 3;
    context.fillRect(rectX, rectY, rectW, rectW);
    context.strokeRect(rectX, rectY, rectW, rectW);

    animationRef = requestAnimationFrame(anim);
  }
</script>
```

The prefetch attribute can be used to give a hint to the browser to retrieve a resource very likely to be needed on the next navigation. An example is as follows:

```
<head>
  <link rel="prefetch" href="prefetch_page.html" as="type"/>
</head>
```
The same applies to images :

```
<head>
  <link rel="preload" href="../images/Tulips.jpg"  as="image"/>
</head>
```

You can do server communications with the Beacom API. It makes use of Ajax to send data to a serve using the XML http request object. Make sure the server communication doesn't interfere with the performance of your app. The Beacon API is useful when you need to send data and you don't require a response. This data is also sent asynchronously. The API consists of a single function names sendBeacon. The syntax is as follows : `navigator.sendBeacon(targetURL, data)` . The function returns a boolean for if the function is able or not to send the data. The API is in a way a replacement for AJAX. We use below PutsReq in order to display the information from the calls :

```
<script>
  const beaconURL = "https://putsreq.com/####";
  function sendEvent(strEvent) {
    if (navigator.sendBeacon) {
      navigator.sendBeacon(beaconURL, strEvent);
    }
  }
  
  window.addEventListener('load', function(e) {
  
    sendEvent("loadEvent")
    document.getElementById("btn1").addEventListener("click", function() {
      sendEvent("Button 1 click");
    });
    document.getElementById("btn2").addEventListener("click", function() {
      sendEvent("Button 2 click");
    });
  })
  
  window.addEventListener('unload', function() {
    sendEvent("unloadEvent")
  })
</script>
```

