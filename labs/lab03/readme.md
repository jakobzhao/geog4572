# Lab 3:  Interactive Map Design

> Spring 2018 | Geography 4/572 | Geovisualization: Geovisual Analytics
>
> **Instructor:** Bo Zhao  **Location:** Wilkinson 210 | **Time:** T 1800 - 1950
>
> **Assigned:** 04/17/2018 | **Due:** `04/24/2018 @11:59pm` | **Points Available** = 50
>
> **Contributors:** [Courtney van Stolk](https://github.com/vanstolc)

In this lab, we will walk through the process of creating a thematic map of  cell towers in Oregon. Then, you will apply these techniques to create a map of airports across the US. Inside the geog4572 git file for Lab 3 you will find a series of 8 HTML files labeled map1 through map8 which show you the correct outcome for each set of steps.

> Throughout the walk-through section areas in this `note` markdown format indicate extra opportunities to explore the many options in Leaflet, Chroma, etc.

When creating a web map, one of the key components is styling your elements to provide proper symbolization for your data. This increases legibility for users and can give your map an appealing, custom design. Elements that can be custom designed include thematic layers (i.e., points, lines, and polygons), base maps (as a leaflet `tileLayer`), interactive features (the components of the map that allow for user interaction), and legends and supplemental information (such as credits, etc.).

Our data for this visualization come from the county boundaries is from [Oregon Explorer](http://oregonexplorer.info) and the spatial distribution of cell towers is from [Map Cruzin](http://www.mapcruzin.com/google-earth-maps-resources/kml/us-cell.kmz). Below is the web map you will make by walking through this lab handout.

![](img/final_map.jpg)

To get started, please synchronize the course material to the working space of your local computer. If you are working in the Digital Earth Lab, please synchronize your course material on the desktop directory.  The material for this lab is located at `[your_working_space]/geog4572/labs/lab03`. Next, open the course material in Webstorm.

## 1. Set up our Map and Add Data

In your IDE (Webstorm), open `map1.html` to prepare for editing.

In this file, you will see a basic HTML page.

Inside the `head` tag, we include both the latest version of `leaflet.css` and `leaflet.js`. After the `leaflet.css` we add a `style` tag in order to include our customized CSS styling codes.

Inside the `body` tag, we put a `map` div tag for holding the map object. After that map `div` tag, we include a `script` tag to put the javascript codes.

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Cell Towers in Oregon (2009)</title>
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.3.1/dist/leaflet.css"/>
    <style>

    </style>
    <script src="https://unpkg.com/leaflet@1.3.1/dist/leaflet.js"></script>
</head>
<body>
<!-- Our web map and content will go here -->
<div id="map"></div>
<script>

</script>
</body>
</html>
```

**Full screen styling**

To expand the map to the full screen, we set the width and height of `html`, `body` and `#map` as `100%`, and no margin, background color as white.

```css
html, body, #map { width: 100%; height: 100%; margin: 0; background: #fff; }
```

**The Script**

Inside the `script` tag,  we create a `mymap` variable to hold the leaflet map object. The first parameter of `L.map` object `'map'` is the `id` of the div to hold the map object.

Next, we add a `tileLayer` to add a base map to the `mymap` variable.

```js
// 1. Create a map object.
var mymap = L.map('map', {
    center: [44.13, -119.93],
    zoom: 7,
    maxZoom: 10,
    minZoom: 3,
    detectRetina: true // detect whether the sceen is high resolution or not.
});

// 2. Add a base map.
L.tileLayer('http://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}.png').addTo(mymap);
```

Please  click the chrome button that appears when you hover your mouse over the top right corner of the editing window in Webstorm. This will open a browser window showing a basic map of the extent of Oregon.

> **Note to people who have done 371/571:** Please think about how to host this html via python SimpleHTTPServer.

![](img/map1.jpg)

The base map (in the format of `tile layer`) is provided by CartoDB. The light color stands out the principal features. If you would like to  switch to other map providers, please refer to [Leaflet providers](http://leaflet-extras.github.io/leaflet-providers/preview/), where you can grab the JavaScript code for a myriad of other base maps!

![](img/leaflet-basemap-providers.JPG)

> **Note:** If the provided base maps do not suit you, you can create custom tiles that can be served to your maps. This topic, on the whole, is large and we will have another series of lectures that introduces creating web map services by GeoServer.

**Add the Cell Towers Data**

Next, we want to add the cell tower data set to the map. Firstly, we need to include another Javascript library [`leaflet.ajax`](https://github.com/calvinmetcalf/leaflet-ajax) in the `head` element. This library will be used to asynchronously read `GeoJson` data.

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/leaflet-ajax/2.1.0/leaflet.ajax.min.js"></script>
```

In the directory `assets`, you will find a geojson file - `cell_towers.geojson`. Enter the following code snippet below the ""// 2. Add a base map section" to add the cell towers to your map.

```js
// 3.Add cell towers GeoJSON Data
// Null variable that will hold cell tower data
var cellTowers = null;
// Get GeoJSON and put on it on the map when it loads
cellTowers= L.geoJson.ajax("assets/cell_towers.geojson");
// Add the cellTowers to the map.
cellTowers.addTo(mymap);
```

The `cellTowers` object hold the GeoJSON data, and then it adds to the `mymap` object. Save and refresh your map. You should see the points populate. That is a lot of cell towers!

Besides, to append some credit information to the Leaflet link at the right bottom corner, we will assign the `attribute` option the credit information. as shown below.

```javascript
attribution: 'Cell Tower Data &copy; Map Cruzin | Oregon counties &copy; Oregon Explorer | Base Map &copy; CartoDB | Made By Bo Zhao'
```

Here, we add credit information about the data source and the map author's information.

Then, please open `map2.html` to see how the map looks like at this stage. Your map should look the same if your edits to **map1.html** have succeeded.

![](img/map2.jpg)

## 2. Point Marker Visualization

Right now, each cell towers is visualized as the default blue marker. To differentiate the cell tower ownership by color, we will introduce how to apply a custom icon using **Font Awesome** and how to make a color scheme with **Chroma.js**.

### 2.1 Create the color scheme for markers

[**Font Awesome**](http://fontawesome.io/) allows you to add icons by CSS classes. To apply Font Awesome, you will need to include its css link in the `head` element of the web map. Despite its name, we will *not* be using fonts from Font Awesome, only icons.

```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.css"/>
```

In addition, we will use another library `chroma.js` to colorize the icon, and utilize `$` of `jQuery` to manipulate `html` elements to add the colored icons. [Chroma.js](https://gka.github.io/chroma.js/) is a javascript library to manipulate colors. Therefore, we need to include both `chroma.js` and `jQuery` in the head tag.

```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.0/jquery.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/chroma-js/1.3.4/chroma.min.js"></script>
```

Furthermore, we also need some predefined color ramp to symbolize geographic features. We are using Chroma to draw from color ramps created by [ColorBrewer](http://colorbrewer2.org/), an online tool designed to help people select good color schemes for maps and other graphics. It provides three types of palettes: sequential, diverging and qualitative.

- Sequential palettes are suited to ordered data that progress from low to high.
- Diverging palettes are suited to centered data with extremes in either direction.
- Qualitative palettes are suited to nominal or categorical data.

![](img/colorbrewer.jpg)

> **Note:** Color palettes and their names are taken from Color Brewer

We'll need to create a set of random colors to represent cell towers of different companies. The color should follow the **qualitative palettes** because these palettes can better visualize the nominal and categorical data. For this lab we'll select the `set2` category. Since there are 9 cell towers in Oregon, we will create nine different colors as shown in **// 4.** in the code snippet below.

To apply these colors, we dynamically build classes with a [for loop](https://www.w3schools.com/js/js_loop_for.asp) and then embed these classes in `style` elements within the body of our HTML document as shown in section **// 5.** below.  The style classes are labelled from `marker-color-1` to `marker-color-9`. Each class include a color `property`. Below is the code snippet.

```javascript
// 4. build up a set of colors from colorbrewer's "set2" category
var colors = chroma.scale('Set2').mode('lch').colors(9);

// 5. dynamically append style classes to this page using a JavaScript for loop. These style classes will be used for colorizing the markers.
for (i = 0; i < 9; i++) {
    $('head').append($("<style> .marker-color-" + (i + 1).toString() + " { color: " + colors[i] + "; font-size: 15px; text-shadow: 0 0 3px #ffffff;} </style>"));
}
```

> **Note:**  Refer to the color palettes from color brewer, and try other palettes such as `Set1`, `Dark2` , etc.

### 2.2 Assign a style class to each company

Next, we will assign a style class to each company. The nine wireless companies are  `New Cingular`, `Verizon`, `Cello`, `Salem Cellular`, etc.  We number the company name from 0 to 8, and then assign the style class (from `marker-color-1` to `marker-color-9`) to markers. If the value of `feature.property.company` is equal to "New Cingular", we set `marker-color-1` class to it, and so on so forth.

Here we use`If.. Else` statements. To do this, we can put a [conditional statement](https://www.w3schools.com/js/js_if_else.asp) to see if the `feature.property.company` is equal to a specific company name.  If it equals, we set the id value, and if not, the else statement will run until it finds the appropriate id value. Below is the code snippet.

```javascript
function (feature, latlng) {
    var id = 0;
    if (feature.properties.company == "New Cingular") { id = 0; }
    else if (feature.properties.company == "Cellco")  { id = 1; }
    else if (feature.properties.company == "RCC Minnesota")  { id = 2; }
    else if (feature.properties.company == "Verizon")  { id = 3; }
    else if (feature.properties.company == "US Cellular")  { id = 4; }
    else if (feature.properties.company == "Hood River Cellular")  { id = 5; }
    else if (feature.properties.company == "Medford Cellular")  { id = 6; }
    else if (feature.properties.company == "Oregon RSA")  { id = 7; }
    else { id = 8;} // "Salem Cellular"
    return L.marker(latlng, {icon: L.divIcon({className: 'fa fa-signal marker-color-' + (id + 1).toString() })});
}
```

### 2.3. Apply an Icon

We apply an icon to each marker. To apply that, you will simply link the class with the marker using the steps outlined below. Notably, a [javascript object or html element can carry multiple classes](https://www.w3schools.com/html/html_classes.asp). In our case, a class `fa` informs that the font awesome will be applied, and another class `fa-signal` informs that an icon showing a signal will be added. And other classes `marker-color-1~9` deal with color, font-size, as well as text-shadow.

> **Note:** If you feel a little confused about the style properties of a class, try to change the property value to some extreme numbers, and then see the differences. For example, you can change the font-size from 15 to 100, and then see what has been changed.

**Use `point to layer` option of `L.geoJson` to set the icon**

We need to create a layer from the GeoJSON point file in order to style it and set the icon for the points. We do this by using the `pointToLayer` option of `L.geoJson`. `pointToLayer` runs a function when the GeoJSON is loaded that takes a feature, latitude, and longitude and creates an L.marker object at that latitude and longitude.

In the snippet below, the phrase fa-signal shows that we're using the "signal" icon from the Font Awesome library. Try changing this to `fa-facebook` to see what happens!  There are many other icon options available on their [website](www.fontawesome.com).

```js
pointToLayer: function (feature, latlng) {
    var id = 0;
    if (feature.properties.company == "New Cingular") { id = 0; }
    else if (feature.properties.company == "Cellco")  { id = 1; }
    else if (feature.properties.company == "RCC Minnesota")  { id = 2; }
    else if (feature.properties.company == "Verizon")  { id = 3; }
    else if (feature.properties.company == "US Cellular")  { id = 4; }
    else if (feature.properties.company == "Hood River Cellular")  { id = 5; }
    else if (feature.properties.company == "Medford Cellular")  { id = 6; }
    else if (feature.properties.company == "Oregon RSA")  { id = 7; }
    else { id = 8;} // "Salem Cellular"
    return L.marker(latlng, {icon: L.divIcon({className: 'fa fa-signal marker-color-' + (id + 1).toString() })});
    }
```

> **Note:** there are *two equal signs (==)*, this is because JavaScript is very particular about operators. To read more, check out this documentation from `w3schools`.

**Options available for `L.geoJson` include**:

- `pointToLayer`: Function that will be used for creating layers for GeoJSON points (if not specified, simple markers will be created).
- `style`: Function that will be used to get style options for vector layers created for GeoJSON features.
- `onEachFeature`: Function that will be called on for each created feature layer. Useful for attaching events and popups to features.
- `filter`: Function that will be used to decide whether to show a feature or not.
- `coordsToLatLng`: Function that will be used for converting GeoJSON coordinates to LatLng points (if not specified, coordinates will be assumed to be WGS84 — standard [longitude, latitude] values in degrees).

In addition to `pointToLayer`, we will use `onEachFeature` option to set the popup.

```js
// assign a function to the onEachFeature parameter of the cellTowers object.
// Then each (point) feature will bind a popup window.
// The content of the popup window is the value of `feature.properties.company`
onEachFeature: function (feature, layer) {
    layer.bindPopup(feature.properties.company);
},
```

 Please open **map3.html** to see how the map looks like. We have changed the icons to cell towers!

![](img/map3.jpg)

## 3. Polygon Visualization

In `assets` directory, you'll see another dataset  `counties.geojson`. This file stores all the counties of Oregon. Each county contains the number of cell towers; this number is pre-calculated in QGIS. To add the data to the map, create another `L.geoJson` object using the `ajax()` method. Enter the following code at the end of your script, staying within the `script` tags.

```js
// create the county layer
L.geoJson.ajax("assets/counties.geojson").addTo(mymap);
```

Save and refresh your map. Counties of Oregon will be displayed on the map, symbolized in a default blue.

![](img/map4-1.jpg)

Let's do something about that default blue and thematically style our data to these polygons useful by turning them into a choropleth layer. The `counties.geojson` file contains numbers of cell towers in each county, calculated in QGIS.  To symbolize the counties  by the number of cell towers, we will use the `style` option that contains styling properties.

### 3.1 Set a sequential color palette

The first step is to set up a function to create color classes. One way to hard code the colors is to make the color scheme via QGIS, selecting some classification rule like Jenk's Natural Breaks, and copy the break numbers as well as color value. Or you can check out a color ramp from [colorbrewer2.org](). In this case, you will use `chroma.js` to dynamically create an array of colors just like you did for the cell tower symbol colors. Since the number of cell towers in each county is ordered data that progresses from low to high, we will use a **sequential color palette** called `OrRd` (meaning from Orange to Red). Then, we develop a `setColor` function that returns the color value using the number of cell towers in a county. Add the following code snippet in the `script` element.

```js
// 6. Set function for color ramp
colors = chroma.scale('OrRd').colors(5); //colors = chroma.scale('OrRd').colors(5);

function setColor(density) {
    var id = 0;
    if (density > 18) { id = 4; }
    else if (density > 13 && density <= 18) { id = 3; }
    else if (density > 10 && density <= 13) { id = 2; }
    else if (density > 5 &&  density <= 10) { id = 1; }
    else  { id = 0; }
    return colors[id];
}
```

> `&&` is a [logic operator combining two comparisons](https://www.w3schools.com/js/js_comparisons.asp).

> We'll be going more into Chroma.js later in the course, but in the meantime you can check out its webpage at http://gka.github.io/chroma.js/ if you're curious!

### 3.2 Apply the color palette

Next, develop a function that will set the style option of the county  `L.geoJson.ajax()` object that you'll insert into the document in *Section 3.3*. We name this function `style` and it can accept a GeoJson feature as it is, without being converted into a layer. Having the feature loaded, this function sets the `fillColor` property with `setColor` function as well as an input value - `feature.properties.CT_CNT`.  Then, we add the following code snippet in the `script` element.

> What's CT_CNT? It's the property in the `counties.json` file that stores the number of cell towers in each county, as shown in the snippet below. We'll talk more about .json in a future lecture, don't worry if you aren't familiar with it now.

```json
{
"type": "FeatureCollection",
"name": "counties",
"crs": { "type": "name", "properties": { "name": "urn:ogc:def:crs:OGC:1.3:CRS84" } },
"features": [
{ "type": "Feature", "properties": { "NAME": "CLATSOP", "CT_CNT": 3 }, "geometry": { "type": "Polygon", "coordinates": [ [ [ -123.6262463,
```



```js
// 7. Set style function that sets fill color.md property equal to cell tower density
function style(feature) {
    return {
        fillColor: setColor(feature.properties.CT_CNT),
        fillOpacity: 0.4,
        weight: 2,
        opacity: 1,
        color: '#b4b4b4',
        dashArray: '4'
    };
}
```

While `fillColor` and `fillOpacity` properties are for the fill; `weight`, `opacity`, `color`, and `dashArray` properties are for the border.

There are many ways to change the color of items in your code. For example, Webstorm allows you to easily change the color by clicking on the "color box" icon to the left of the line of code.

![](img/webstormcolorchange.JPG)

### 3.3 Set style option

The final step is to set the style option for the county layer. Below shows the code of adding the county polygons to the map, and also applying the style.

```js
// 8. Add county polygons
L.geoJson.ajax("assets/counties.geojson", {
    style: style
}).addTo(map);
```

Save and refresh the html page. Open `map4.html`  to see our styled polygons! If you're on the right track the two should look the same.

![](img/map4.jpg)

## 4. Map Elements

Now we add a legend to help the audience to read this map. To do that, the main Leaflet object is the `Control` object, or `L.control`. It allows for adding various elements to your map.

### 4.1 Add a Legend

Adding a legend is easy, but requires quite a bit of code. The workflow to create a legend involves creating a Leaflet control, setting the control to populate with HTML that represents the legend components, and styling the HTML with CSS so they appear properly on our screen. I'm going to throw a bit more code at you this time, and we will walk through what it is doing. Enter the following block of code to your `script` (stay in those script tags!).

```js
// 9. Create Leaflet Control Object for Legend
var legend = L.control({position: 'topright'});

// 10. Function that runs when legend is added to map
legend.onAdd = function () {

    // Create Div Element and Populate it with HTML
    var div = L.DomUtil.create('div', 'legend');
    div.innerHTML += '<b># Cell Tower</b><br />';
    div.innerHTML += '<i style="background: ' + colors[4] + '; opacity: 0.5"></i><p>19+</p>';
    div.innerHTML += '<i style="background: ' + colors[3] + '; opacity: 0.5"></i><p>14-18</p>';
    div.innerHTML += '<i style="background: ' + colors[2] + '; opacity: 0.5"></i><p>11-13</p>';
    div.innerHTML += '<i style="background: ' + colors[1] + '; opacity: 0.5"></i><p> 6-10</p>';
    div.innerHTML += '<i style="background: ' + colors[0] + '; opacity: 0.5"></i><p> 0- 5</p>';
    div.innerHTML += '<hr><b>Company<b><br />';
    div.innerHTML += '<i class="fa fa-signal marker-color-1"></i><p> New Cingular</p>';
    div.innerHTML += '<i class="fa fa-signal marker-color-2"></i><p> Cello</p>';
    div.innerHTML += '<i class="fa fa-signal marker-color-3"></i><p> RCC Minnesota</p>';
    div.innerHTML += '<i class="fa fa-signal marker-color-4"></i><p> Verizon</p>';
    div.innerHTML += '<i class="fa fa-signal marker-color-5"></i><p> US Cellular</p>';
    div.innerHTML += '<i class="fa fa-signal marker-color-6"></i><p> Hood River Cellular</p>';
    div.innerHTML += '<i class="fa fa-signal marker-color-7"></i><p> Medford Cellular</p>';
    div.innerHTML += '<i class="fa fa-signal marker-color-8"></i><p> Oregon RSA</p>';
    div.innerHTML += '<i class="fa fa-signal marker-color-9"></i><p> Salem Cellular</p>';
    // Return the Legend div containing the HTML content
    return div;
};

// 11. Add a legend to map
legend.addTo(mymap);
```

So, what did we do here?

- First, we created an instance of a  **Leaflet Control object**, calling it 'legend', and used the position option to tell it to locate in the top right of our map.
- Next, we used the `onAdd` method of the control to run a function when the legend is added. That function created a new div in the DOM, giving it a class of legend. This allowed the CSS to style everything using the legend element.
- In the newly created div, we are going to populate it with HTML by using a built-in JavaScript DOM method called innerHTML. Using innerHTML allows us to change the content of the HTML and add to the legend div. Using the plus-equal `+=` instead of equal `=` is the syntax for append. Every time this is used, code following is appended to existing code. In this, we write the HTML we want to use in our legend. Note, the `i` tag represents our legend icons.
- Within the HTML, fill in the colors and ranges so that they match our data classification.
- After the HTML is appended, return the div element.
- Lastly, add the legend to the map.

> **Note:** Instead of using innerHTML, what in jQuery can we use to do the same task?

**Use CSS to Style**

If we save and refresh, the items you see won't make much sense. We need to use CSS to give them placement and organization on the page. The following CSS code will style our legend elements. Enter it between the style tags in the head of your HTML document. Like above, we'll then walk through what it does.

```css
.legend {
    line-height: 16px;
    width: 140px;
    color: #333333;
    font-family: 'Open Sans', Helvetica, sans-serif;
    padding: 6px 8px;
    background: white;
    background: rgba(255,255,255,0.5);
    box-shadow: 0 0 15px rgba(0,0,0,0.2);
    border-radius: 5px;
}

.legend i {
    width: 16px;
    height: 16px;
    float: left;
    margin-right: 8px;
    opacity: 0.9;
}

.legend img {
    width: 16px;
    height: 16px;
    margin-right: 3px;
    float: left;
}

.legend p {
    font-size: 12px;
    line-height: 16px;
    margin: 0;
}
```

First, we set properties for the legend using `.legend` to style the legend class. We set a line height, color, font, padding, background, drop shadow, and border corner radius. Next we set our icon (`i`) tag, this should be set to float: left; so that elements will align into columns, then we set properties for the image (`img`) tag, making them the same size and giving them the same float as the icons. Lastly, we style our paragraph tag (`p`), making sure line-height is consistent with the others. Save and refresh your map. You should see your styled legend applied to your map.

### 4.2 Add a Scale Bar

The Leaflet Control object allows you to add a number of elements, including attribution and zoom controls. To add a scale bar, please enter the following line to add a scale bar to your map.

```js
// 12. Add a scale bar to map
L.control.scale({position: 'bottomleft'}).addTo(mymap);
```

Save and refresh the html page. Open `map4.html`  to see the legend and scale bar.

### 4.3 Change the fonts

Choosing fonts is an important part of cartography, and an often overlooked one. Right now, our map uses the default Browser font, usually Times New Roman. To edit fonts, we want to style CSS. In CSS, there are a lot of options for fonts, for more reading, check out the [w3schools font documentation](http://www.w3schools.com/css/css_font.asp).

Traditionally, a font is loaded into your page only if you have it on your computer. This presents a problem though, if someone doesn't have the font, it will change the page to use secondary or default fonts. In order to ensure that every visitors computer display the same, you can link to online font libraries. A common, useful online font library is Google Fonts. Google fonts can be added to any site, and since you link to the style, you don't have to worry about the user not having the font installed on their computer. Check out the [Google Font library](fonts.google.com) and explore their options. Let's link a common web font called `Titillium Web` to our document so we can use it. To link it to our document, enter the following line of code into the head section of your document. It should go right after your stylesheets.

```html
<head>...
<link href="https://fonts.googleapis.com/css?family=Titillium+Web" rel="stylesheet">
...</head>
```

Next, to style all text in our document with the `Titillium Web` font, modify the `.legend` tag in the CSS (the code between the style tags). Modify the body CSS properties to look like the following, adding a font-family property after margin.

```html
.legend {
    ...
    font-family: 'Titillium Web', sans-serif;
    ...
}
```

Save and refresh your map. Or open `map5.html`.  `Titillium Web` will now be your preferred font for legend panel!

**Style the credits using CSS**

Lastly, to help you explore the power of CSS, style the credits at the bottom of your page. Because the div containing the credits has `id="credits"`, we can style it using #credits. All of the contents in the credits div are between two paragraph tags. CSS styling is written in a nested fashion, to style everything that is in a p element within the `#credits div`, we use `#credits p`. Add the following snippet between the style tags in the head section of the document.

```css
#credits p {
	margin-top: 5px;
	font-size: 12px;
	text-align: left;
	line-height: 16px;
}
```

Save and refresh your map. Or open `map5.html`.  `Titillium Web` will now be your preferred font for legend panel!

![](img/map5.jpg)

> A few cartographic notes to keep in mind - try to avoid using more than 3 fonts on a map, and stick to all serif or all sans-serif.

### 5. Advanced Features (Optional)

***If you have not taken GEOG 371 or 571 before, you can skip this section and directly go to the deliverable.***

#### 5.1 Add Graticules

Inside the `head` tag, please add a new javascript library after the `chroma.js` library.

```javascript
<head>
    ...
    <script type="text/javascript" src="https://cloudybay.github.io/leaflet.latlng-graticule/leaflet.latlng-graticule.js"></script>
</head>
```

Append the end of the script code, add the following code snippet.

```javascript
// 13. Add a latlng graticules.
L.latlngGraticule({
    showLabel: true,
    opacity: 0.2,
    color: "#747474",
    zoomInterval: [
        {start: 2, end: 7, interval: 2},
        {start: 8, end: 11, interval: 0.5}
    ]
}).addTo(mymap);
```

The object `L.latlngGraticule` is provided by the `leaflet.latlng-graticule.js` library. Its options such as `showLabel`, `opacity`, `color` are straightforward to understand.  As for `zoomInterval`,  `{start: 2, end: 7, interval: 2}` means, from the zoom level 2 to 7, both the latitude and longitude interval is 2 degree, while ` {start: 8, end: 11, interval: 0.5}` means,  from zoom level 8 to 11,  both the latitude and longitude interval is 0.5 degree. For more information about this Graticules library, please visit [https://github.com/cloudybay/leaflet.latlng-graticule](https://github.com/cloudybay/leaflet.latlng-graticule).

- **showLabel**: Show the grid tick label at the edges of the map. Default `true`
- **opacity**: Opacity of the Graticule and Label. Default `1`
- **weight**: The width of the graticule lines. Default `0.8`
- **color**: The color of the graticule lines. Default `#aaa`
- **font**: you can change the font Style for the tick label. Default `12px Verdana`
- **fontColor**: you could also change the color of the tick label. Default `#aaa`

#### Special Options

Some of the projections (like Lambert) require graticules that are not straight lines; set those options to draw a polyline graticule.

- **lngLineCurved**: Interval of polyline. Default `0`
- **latLineCurved**: Interval of polyline. Default `0`

Check out the [Lambert projection example](https://cloudybay.github.io/leaflet.latlng-graticule/example/lambert.html).

Save and refresh your map. Or open[ `map6.html`](.  Graticules are applied!

![](img/map6.jpg)

#### 5.2 Add Dynamic Labels

The label function is supported by the [**Label Gun**](https://github.com/Geovation/labelgun) library, which is a mapping library agnostic labelling engine. It allows you to avoid cluttering in mapping popups and labels, providing precedence to labels of your choice. The library makes three assumptions:

- Each label has a bounding rectangle (Min X, Min Y, Max X, Max Y)
- Each label has a weight
- You can provide a function that will hide and show a label (e.g. changing a CSS class or calling a mapping library method)

To use this library, in your `head` tag, add two libraries `rbush.min.js` and `labelgun.min.js ` **in front of** the `leaflet.js`, as shown below:

```html
<head>
    ...
    <script src="https://unpkg.com/rbush@2.0.1/rbush.min.js"></script>
    <script src="https://unpkg.com/labelgun@6.0.0/lib/labelgun.min.js"></script>
    <script src="https://unpkg.com/leaflet@1.3.1/dist/leaflet.js"></script>
    ...
</head>
```

Then, inside the `style` tag, define the label font style.

```css
.leaflet-tooltip.feature-label {
    background-color: transparent;
    border: transparent;
    box-shadow: none;
    font-weight: bold;
    font-size: 12px;
    font-family: 'Titillium Web', sans-serif;
    text-shadow: 0 0 2px #FFFFFF;
    color: rgba(35, 35, 35, 0.78)
}
```

To add dynamic label, we will create variables to show or hide Label,  an array to hold labels, and the label engine. We create these variables prior to create the map variable.

```javascript
// 14. This is core of how Labelgun works. We must provide two functions, one
// that hides our labels, another that shows the labels. These are essentially
// callbacks that labelgun uses to actually show and hide our labels
// In this instance we set the labels opacity to 0 and 1 respectively.
var hideLabel = function(label){ label.labelObject.style.opacity = 0;};
var showLabel = function(label){ label.labelObject.style.opacity = 1;};
var labelEngine = new labelgun.default(hideLabel, showLabel);
var labels = [];
```

Then, we will create a label for each county. The label will be the county name `feature.properties.NAME`.

```javascript
// 15. Create a label for each county.
var counties = null;
counties = L.geoJson.ajax("assets/counties.geojson", {
    style: style,
    onEachFeature: function (feature, label) {
        label.bindTooltip(feature.properties.NAME, {className: 'feature-label', permanent:true, direction: 'center'});
        labels.push(label);
    }
}).addTo(mymap);
```

Next, we create an `addLabel` function to dynamically update the visible labels, aiming to avoid the label overlap.  You do not need to know the specific meaning of this function, but please make sure to capture the bounding box from the `mymap` variable.

> What does it mean to capture the bounding box? While you don't have to understand all of this code, be sure that the variable `mymap` here has to refer to the name of your bounding box in Leaflet set in section `// 1.` of the code.

```javascript
function addLabel(layer, id) {
    // This is ugly but there is no getContainer method on the tooltip :(
    var label = layer.getTooltip()._source._tooltip._container;
    if (label) {
        // We need the bounding rectangle of the label itself
        var rect = label.getBoundingClientRect();

        // We convert the container coordinates (screen space) to Lat/lng
        var bottomLeft = mymap.containerPointToLatLng([rect.left, rect.bottom]);
        var topRight = mymap.containerPointToLatLng([rect.right, rect.top]);
        var boundingBox = {
            bottomLeft : [bottomLeft.lng, bottomLeft.lat],
            topRight   : [topRight.lng, topRight.lat]
        };

        // Ingest the label into labelgun itself
        labelEngine.ingestLabel(
            boundingBox,
            id,
            parseInt(Math.random() * (5 - 1) + 1), // Weight
            label,
            label.innerText,
            false
        );

        // If the label hasn't been added to the map already
        // add it and set the added flag to true
        if (!layer.added) {
            layer.addTo(mymap);
            layer.added = true;
        }
    }

}
```

At last, we will update the visualization of the labels whenever you zoom the map.

```javascript
mymap.on("zoomend", function(){
    var i = 0;
    counties.eachLayer(function(label){
        addLabel(label, ++i);
    });
    labelEngine.update();
});
```

Save and refresh the map, or open `map7.html`, the dynamic labels are added! Please zoom in and out and see how the visualization of labels changes.

![](img/map7.jpg)

#### 5.3 Reproject a web map

Most of publicly shared base map are projected in Web Mercator (a.k.a Google Mercator). In order to use a custom projection, we need to follow the procedure below

First of all, include the two necessary libraries `proj4js` and `proj4leaflet`  after the `leaflet.js`

```html
<head>
	...
    <script src="https://unpkg.com/leaflet@1.3.1/dist/leaflet.js"></script>
	...
    <script src="https://cdnjs.cloudflare.com/ajax/libs/proj4js/2.4.4/proj4.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/proj4leaflet/1.0.2/proj4leaflet.min.js"></script>
	...
</head>
```

Then, we need to find the appropriate projection for Oregon. To do that, go to [http://spatialreference.org/](http://spatialreference.org/), and search “Oregon” on the search input on the top right.

For the list of projections, we choose "[EPSG:2991](http://spatialreference.org/ref/epsg/2991/): NAD83 / Oregon Lambert", click into the [web page for EPSG:2991](http://spatialreference.org/ref/epsg/2991/), and then click the `proj4` link in the grey box.

![](img/spatial-reference.JPG)

Once you click on the [Proj4](http://spatialreference.org/ref/epsg/2991/) item, you will have the following text appear in the window:

```javascript
+proj=lcc +lat_1=43 +lat_2=45.5 +lat_0=41.75 +lon_0=-120.5 +x_0=400000 +y_0=0 +ellps=GRS80 +datum=NAD83 +units=m +no_defs
```

So, we can define our custom CRS as `mycrs` as below.

```javascript
// 18. define the coordinate reference system (CRS)
mycrs = new L.Proj.CRS('EPSG:2991',
    '+proj=lcc +lat_1=43 +lat_2=45.5 +lat_0=41.75 +lon_0=-120.5 +x_0=400000 +y_0=0 +ellps=GRS80 +datum=NAD83 +units=m +no_defs',
    {
        resolutions: [8192, 4096, 2048, 1024, 512, 256, 128, 64, 32, 16, 8, 4, 2, 1] // example zoom level resolutions
    }
);
```

Here, the resolution array is listed for creating zoom level 1 to 14 (There are 14 resolutions). If you are not familiar with the resolution array, you can just input the array above by default. For more information about how to use  `L.Proj.CRS`, please refer to http://kartena.github.io/Proj4Leaflet/api/.

 After the custom projection is created, you will need to assign it to the `crs` option of the map. Also, since the map follows a new zoom level system, we need to update the zoom level. If you do not know which one should use, you can just test different zoom level from 0 to 14 to find the best fit. See the code snippet below.

```javascript
var mymap = L.map('map', {
    crs: mycrs, // 19. assign the custom crs to the crs option. change the zoom levels due to the change of projection.
    center: [44.13, -119.93],
    zoom: 3, // we choose zoom level 3
    maxZoom: 10,
    minZoom: 3,
    detectRetina: true});
```

Because the scale bar does not work properly after a reprojection, we need to comment off the scale bar (in step 12) with the two-backslash syntax. Also, since most publicly shared base map only support web Mercator, we should comment off the base map (in step 2) as well. See the code snippet below.

```javascript
// 2. comment off the base map, because the publicly shared base map usually cannot reprojected
// L.tileLayer('http://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}.png').addTo(mymap);
...
// 12. comment off the scale bar, because in same projection, scalebar does not make sense.
// L.control.scale({position: 'bottomleft'}).addTo(mymap);
```

Then, the final map is done! Please open `map8.html` to see the web map in Oregon Lambert projection!

![](img/final_map.jpg)

## 6. Deliverable

**For the student who has not taken GEOG 371 or 571**

After you successfully deploy this cell tower map, you are expected to build another web map of airports in United States. In the `assets` directory of this lab, you will see two geojson files: one is [`airports.geojson`](assets/airports.geojson), another is [`us-states.geojson`](assets/us-states.geojson).

`airports.geojson` contains all the airports in United States. This data is converted from a shapefile, which was downloaded and unzipped from https://catalog.data.gov/dataset/usgs-small-scale-dataset-airports-of-the-united-states-201207-shapefile. For each airport feature, the field `CNTL_TWR` indicates whether the airport has an air traffic control tower or not. If there is a tower, the value of `CNTL_TWR` is 'Y', otherwise 'N'. You may need to find an appropriate icon on `font awesome`. **(6 points)**

`us-states.geojson` is a geojson data file containing all the states boundaries of United States. This data is acquired from from [Mike Bostock](http://bost.ocks.org/mike) of [D3](http://d3js.org/). The `count` field indicates the number of airports within the boundary of the state under investigation. So please make a choropleth map based on the number of airports within each state.  **(5 points)**

Regarding the grading criteria, this web map of airports needs include:

- an appropriate basemap;  **(5 points)**
- some interactive elements, like a clickable marker; **(7 points)**
- some map elements, such as legend, scale bar, credit;  **(8 points)**

**For student who has already taken GEOG 371 or 571, or he who wants to challenge yourself**

After you successfully deploy this cell tower map, you are expected to build another web map of airports in United States. In the `assets` directory of this lab, you will see two geojson files: one is [`airports.geojson`](assets/airports.geojson), another is [`us-states.geojson`](assets/us-states.geojson).

`airports.geojson` contains all the airports in United States. This data is converted from a shapefile, which was downloaded and unzipped from https://catalog.data.gov/dataset/usgs-small-scale-dataset-airports-of-the-united-states-201207-shapefile. For each airport feature, the field `CNTL_TWR` indicates whether the airport has an air traffic control tower or not. If there is a tower, the value of `CNTL_TWR` is 'Y', otherwise 'N'. You may need to find an appropriate icon on `font awesome`. **(3 points)**

`us-states.geojson` is a geojson data file containing all the states boundaries of United States. This data is acquired from from [Mike Bostock](http://bost.ocks.org/mike) of [D3](http://d3js.org/). The `count` field indicates the number of airports within the boundary of the state under investigation. So please make a choropleth map based on the number of airports within each state.  **(3 points)**

Regarding the grading criteria, this web map of airports needs include:

- an appropriate projection;  **(7 points)**
- Graticules; **(5 points)**
- dynamic labels of the state name; **(6 points)**
- some interactive elements, like a clickable marker; **( 3 points)**
- Legend;  **(5 points)**

## Submission

- you will need to synchronize this project to a GitHub repository. And make sure the web map is accessible from a url link, which should be similar to `http://[your_github_username].github.io/[your_repository_name]/index.html`. (You may want to check out previous lecture or lab handouts on project management and hosting via GitHub); **(6 points)**

- To simplify your html page, please put the javascript code in the script tag to a separate javascript file `main.js` under the `js` folder, and put the CSS code in the style tag to a separate CSS file `main.css` under the `css` folder. If you will use any images or videos, please put to the `img` folder, where the geojson data are in the `assets` folder.  Please make sure the project repository structure is well organized. It should be similar to the file structure below. **(4 points)**

  ```powershell
  [your_repository_name]
      │index.html
      │readme.md
      ├─assets
      │      airports.geojson
      │      us-states.geojson
      ├─css
      │      main.css
      ├─img
      │      xxx.jpg
      └─js
              main.js
  ```

- write up a project description in the `readme.md` file. This file will introduce the project name, a brief introduction, the major functions (especially the function which was not covered in the lectures), libraries, data sources, credit, acknowledgement, and other necessary information. **(8 points)**

 For submission, you are expected to submit the **url of the GitHub repository** to the **Canvas Lab 3 submission page** of this course. This url should be in the format of `https://www.github.com/[your_github_username]/[your_repository_name]`. Also the TA and other audience should be able to visit your interactive web map through the url `https://[your_github_username].github.ip/[your_repository_name]`. Please contact the instructor if you have any difficulty in submitting the url link.

> If you have a genuine reason(known medical condition, a pile-up of due assignments on other courses, ROTC,athletics teams, job interview, religious obligations etc.) for being unable to complete work on time, then some flexibility is possible. However, if in my judgment you could reasonably have let me know beforehand that there would likely be a delay, and then a late penalty will still be imposed if I don't hear from you until after the deadline has passed. For unforeseeable problems,I can be more flexible. If there are ongoing medical, personal, or other issues that are likely to affect your work all semester, then please arrange to see me to discuss the situation. There will be NO make-up exams except for circumstances like those above.

## Reference

[1] Map Symbolization http://duspviz.mit.edu/web-map-workshop/map-symbolization/

[2] Data source: http://www.mapcruzin.com/google-earth-maps-resources/google-earth-cell-towers.htm

[3] Boundary: http://oregonexplorer.info/ExternalContent/SpatialDataForDownload/RCE_counties.zip

[4] Add topojson instead of geojson http://blog.webkid.io/maps-with-leaflet-and-topojson/