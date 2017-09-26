 1. Select change():

```javascript
var CLOCK = (function() {
    var drawClock = function() {
        var initial = 250;
        var zoom = document.getElementById("rangeinput").value;
        console.log(zoom);
        var value = initial * zoom;
        // Draw Circle
        var svg = document.getElementById("clock");
        svg.setAttribute('width', value);
        svg.setAttribute('height', value);
    };
    return {
        init: function() {
            drawClock();
        },
        zoom: function() {
            drawClock();
        }
    };
})();
CLOCK.init();
```
