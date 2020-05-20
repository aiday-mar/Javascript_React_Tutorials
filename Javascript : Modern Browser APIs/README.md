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
The InterSection Observer API allows us to regulate the visibility of an element, as follows :

```
<script>
  window.addEventListener("load", function() {
    
    const observer = new IntersectionObserver(function (entries) {
      console.log(entries);
      if (entries[0].intersectionRatio < 0.5) {
        entries[0].target.className = "background0";
      }
      if (entries[0].intersectionRatio >= 0.5 &&
          entries[0].intersectionRatio < 1) {
        entries[0].target.className = "background50";
      }
      if (entries[0].intersectionRatio >= 1) {
        entries[0].target.className = "background100";
      }
    },
    {
      "threshold" : [0, 0.5, 1.0]
    })
    
    observer.observe(document.getElementById("targetElem"));
  })
</script>
```

There are various ways to store and manipulate data. This can be done through cookies, application cache, local storage, session storage, XML HTTP requests, Indexed DBs and WebSQL. The Fetch() API can be a replacement for the XML HTTP reuest method. There is also an API provided by the Mozilla foundation called localForage. This API gives a nice wrapper around the IndexedDB API. There is also a Cache API which can be used to cache HTTP requests and response pairs locally. This can be wrapper up with the StorageManager and DeviceMemory APIs, which can be used to determine how much storage space and memory capacity a device has, and how to make it persistent on the user's local machine.

```
<script>
  window.addEventListener("load", function() {
    
    fetch("https://httpbin.org/json").then(function(response) {
      console.log("Content-type :", response.header.get("Content-Type"));
      console.log("Redirected: ", response.redirected);
      console.log("Status: ", response.status);
      console.log("Status-text: ", response.statusText);
      console.log("Response type:", response.type);
      console.log("Response URL:", response.url);
      
      if(response.type == 200) {
        return response.text();
      }.then(function (returnedData) {
        console.log("Returned data : ", returnedData);
      }).catch(function (error) { 
        console.log("Error : ", error);
      })
      
      fetch("https://httpsbin.org/post", {
        method : 'post',
        body: 'foo-bar',
        headers : {
          "x-custom-header" : "my custom value" 
        }
      }).then(function (response) {
        return response.text();
      }).then(function (returnedData) {
        console.log("Returned post data : ", returnedData);
      })
  });
</script>
```
IndexedDB is asynchronous, it keeps web apps responsive, unlike localStorage API. This IndexedDB can store multiple types of data, and is not limited to text strings. They can easily handle multiples separate data stores. The API for using IndexedDB is complex. Next we can use the localForage library as follows. First you need to import it : `<script src="localforage.min.js"></script>`. The following are examples of code snippets using local forage.

```
localforage.setItem(key, val);
localforage.getItem(key);
localforage.removeItem(key);
localforage.iterate(function(value, key, iterNum) {
  console.log(iterNum, [key, value]);
});
```

After each such experssionn above you can add at the end : `.then(function(params){ console.log(" some text ") });`. LocalForage can also support multiple database instances : 

```
var instance1, instance2
document.getElementById("btnMulti").addEventListener("click", function () {
  instance1 = localforage.createInstance({
    "name" : "instance1"  // which is the data present in the local forage
  });
  instance2 = localforage.createInstance({
    "name" : "instance2"
  });
  
  document.getElementById("btnStore").addEventListener("click", function() {
    instance1.setItem("key1", "value1");
    instance2.setItem("key1", "value2");
  });
  
  document.getElementById("btnGetData").addEventListener("click", function () {
    instance1.getItem("key1").then(function (val) {
      console.log("instance1 returned :", val);
    })
    instance2.getItem("key1").then(function (val){
      console.log("instance2 returned :", val);
    })
  });
})
```

We can store data locally using the Cache API. The Cache API takes the results of an HTTP request, and stores it for later use. You can cache anything an HTTP response comes back with.

```
document.getElementById('btnClear').addEventListener("click", function () {
  caches.delete('my-data-cache').then(function(result) { 
    console.log(result ? "cache deleted" : "error" )
  })
});

function getJSONData(url) {
  
  // the following code shows us that the Cache API is there
  if ('caches' in window) { 
    window.caches.open('my-data-cache').then(function (cache) {
      cache.match(url).then(function(result){
        if (result === undefined) {
          console.log("not found in cache: ", url);
          
          fetch(url).then(function (result) { 
            
            let clonedresp = result.clone();
            cache.put(url, result);
            clonedresp.text().then(function(data) { console.log(data) })
            
          });
        }
        else {
          result.text().then(function(text) {
            console.log("cache hit : ", url, text);
          })
        } 
      })
    })
  }
  
}
```
We can get device memory information as follows :

```
if (navigator.deviceMemory) {
  document.getElementById("devMen").textContent = navigator.deviceMemory;
}
```
We show an example of the Dialog API :

```
<dialog id="dialog1">
  <div id="dlgcontent">
    <button id="okBtn">OK</button>
    <button id="cancelBtn">Cancel</button>
  </div>
</dialog>

<script>
  window.addEventListener("load", function() {
    document.getElementById("show1").addEventListener("click", function () {
      document.getElementById("dialog1").show();
    })
    document.getElementById("show2").addEventListener("click", function () {
      document.getElementById("dialog1").showModal();
    })
    
    document.getElementById("okBtn").addEventListener("click", function () {
      dlg = document.getElementById("dialog1");
      
      if(dlg.open) {
        dlg.close("OK");
      }
    })
    
    document.getElementById("cancelBtn").addEventListener("click", function () {
      dlg = document.getElementById("dialog1");
      
      if (dlg.open) {
        dlg.close("Cancel");
      }
    })
    
    dlg = document.getElementById("dialog1");
    dlg.addEventListener("close", function (evt) {
      console.log("Dialog close: ", dlg.returnValue)
    });
    dlg.addEventListener("cancel", function (evt) {
      console.log("Dialog canceled: ", dlg.returnValue)
    });
  })
</script>
```

In JavaScript it is also possible to implement notifications. Example of use :

```
<script>
  window.addEventListener("load", function () {
    Notification.requestPermission().then(function (result) {
      console.log("Notification permission request: ", result);
    })
  })
  
  document.getElementById("btnShow1").addEventListener("click", function() {
    if (Notification.permission == "granted") {
      var notify = new Notification("This is a basic notification");
    }
  })
  
  document.getElementById("btnShow2").addEventListener("click", function() {
    if (Notification.permission == "granted") {
      var title = document.geElementById("notTitle").value;
      var body = document.getElementById("notBody").value;
      var useIcon = document.getElementById("notIcone").checked;
      var isPersistent = document.getElementById("notPersist").checked;
      
      var notOptions = {};
      notOptions.body = body;
      notOptions.requireInteraction = isPersistent;
      if (useIcon) {
        notOptions.icon = "../images/info.png"
      }
      
      var theNote = new Notification(title, notOptions);
      
      theNote.onclick = function (evt) {
        evt.target.close();
        window.location = "http://w3.org"
      }
    }
  })
</script>
```

We can also detect network conditions. An example is as follows :

```
<script>
  window.addEventListener("load", updateNetState);
  window.addEventListener("online", updateNetState);
  window.addEventListener("offline", updateNetState);
  
  function updateNetState(evt){
    const statusElem = document.getElementById("netState");
    let isOnline = navigator.onLine;
    
    statusElem.className = isOnline ? "onlineState" : "offlineState";
    statusElem.innerText = isOnline ? "ONLINE" : "OFFLINE";
    
    if (navigator.connection) {
      connType = navigator.connection;
      statusElem.innerText += " Effective type: " + connType.effectiveType 
      + ", Downlink speed: " + connType.downlink + "MB/s" + 
      ". Estimated round-trip time is: " + connType.rtt + "ms"
    }
  }
</script>
```
We can work with the page visibility as follows :

```
<div id="targetElem">
</div>

<script>
  window.addEventListener("load", function () {
    outputDiv = document.getElementById("targetElemt");
    outputDiv.innerHTML += "<p>Visibility state : " + document.visibilityState + "</p>";
    
    document.addEventListener("visibilitychange", function (evt) {
      outputDiv.innerHTML += "<p>Visibility state : " + document.visibilityState + "</p>";
    })
  })
</script>
```

And we can also make images come full screen.

```
<button id="btnDocFs">Enter Document Fullscreen Mode</button>
<button id="btnIngFs">Enter Image Fullscreen Mode</button>
<button id="btnExitFs">Exit Fullscreen Mode</button>

<script>
  window.addEventListener("load", function() {
  
    document.getElementById("btnDocFs").addEventListener("click", function () {
      enterFullscreen(document.documentElement);
    })
    
    document.getElementById("btnImgFs").addEventListener("click", function () {
      enterFullscreen(document.getElementById("targetImg"));
    })
    
    document.getElementById("btnExitFs").addEventListener("click", function () {
      exitFullscreen();
    })
 })
  
  function enterFullscreen(elem) {
    if (elem.requestFullscreen) {
      elem.requestFullscreen();
    }
    if (elem.webkitRequestFullscreen) {
      elem.webkitRequestFullscreen();
    }
    if (elem.mozRequestFullScreen) {
      elem.mozRequestFullScreen();
    }
    if (elem.msRequestFullScreen) {
      elem.msRequestFullscreen();
    }
  };
  
  function exitFullscreen() {
    if (document.exitFullscreen) {
      document.exitFullscreen();
    }
    if (document.webkitExitFullscreen) {
      document.webkitExitFullscreen();
    }
    if (document.mozCancelFullScreen) {
      document.mozCancelFullScreen();
    }
    if (document.msExitFullscreen) {
      document.msExitFullscreen();
    }
  }
</script>
```
