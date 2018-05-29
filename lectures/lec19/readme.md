# Vector Field

> Spring 2018 | Geography 4/572 | Geovisualization: Geovisual Analytics
>
> **Instructor:** Bo Zhao  **Location:** WITH 205 | **Time:** TR 1100 - 1150

> **Contributors：** Brandi Black, Lila Leatherman, Brian Katz


## Project Q&A:

Please refer to the `layout` folder under the [troubleshoot](../../troubleshoot/layout) folder.

### 1 legend

### 2 button

### 3 model

- fullscreen `lab 03` and `the storymap template of lab`

**fullscreen**

```css
html, body, #map { width: 100%; height: 100%; margin: 0; background: #fff; }
``` 

**leaflet `div` placeholder/element inside a `div` element**


```css
.storymap-map {
    position: fixed;
    top: 0;
    bottom: 0;
    right: 0;
    min-width: 100%;
    min-height: 100%;
    z-index: 900;     /*a larger z-index than the container*/
    display: block;
    overflow-x: hidden;
    overflow-y: hidden;
    background-color: #f5f5f5;
}
```


Refresh the map if the browser windows are resized.

```javascript
 map.invalidateSize();
```

 
### 4 font family in a chart  The `!important` rule


> **Note:** In your css stylesheet, a rule that has the `!important` property will always be applied no matter where that rule appears in the CSS document.