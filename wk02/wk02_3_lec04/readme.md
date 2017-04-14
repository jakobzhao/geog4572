# Web Map Basics


> Spring 2017 | Geography 472/572 | Geovisualization: Geovisual Analytics
>
> Instructor: Bo Zhao | TA: Kyle R. Hogrefe | Location: LINC 368 | Time: Thursday 9-9:50am

**Learning Objectives**

- Use Leaflet to create a map, geographic feature;
- Link external javascript libs to a web map application;
- Add geospatial data to a leaflet based map;
- Add interactive elements; and
- Understand the basics of map events.

This week, we move forward to make a web map from scratch! To do that, this lecture starts with introducing Leaflet - a Javascript library used to create interactive, web-based, mobile-friendly maps. With Leaflet, you can create a simple map in as little as three lines of code, or you can build complex, dynamic, and complex maps that contain hundreds of lines. This lecture assumes you have a working knowledge of HTML, CSS and JavaScript.

## 1. Introduction

A digital map is a map on a computer, a web map is depends on the internet. It is usually interactive, and not always self-contained, meaning it can **grab components from other locations on the web**. The two big concepts are **tiles**, which are gridded images that make up the *basemaps*, and **geographic features**, which can be points, lines/polylines, and polygons, are used for displaying thematic layers. Tiles are static and non-interactive, while the geographic features layers can be dynamic and offer user interaction.

### 1.1 What is Leaflet?

Leaflet is an open-source JavaScript library for interactive web maps. It's lightweight, simple, and flexible, and is probably the most popular open-source mapping library at the moment. Leaflet is developed by Vladimir Agafonkin (currently of MapBox) and other contributors.

What Leaflet does web maps with tiled base layers, panning and zooming, and feature layers that you supply. It handles various basic tasks like converting data to map layers and mouse interactions, and it's easy to extend with plugins. It will also work well across most types of devices.

We will start with an empty webpage, then progressively add components to make a Leaflet map. It assumes a basic knowledge of HTML and JavaScript, or at the very least assumes the will to tinker with the code to better understand what it does. It won't explain every little object or array, but will contain plenty of links. Many code blocks will show only a snippet of code, highlighting the changes over previous examples.

### 1.2 Use an IDE and start up a Web Server

Use an IDE for writing your code, such as **Webstorm**, **Sublime Text**,  or **Notepad++**. To put your map on the web, you need to host the web page and geospatial data to the server. So, you need to transfer the web pages and data to the remote server or to set up the local computer as a server. Regarding setting up a local server, you can try Webstorm debugging/execution environment or python SimpleHTTPServer, such as:

```bash
$ python -m SimpleHTTPServer 8000
```

Now open a browser and access your site at: http://localhost:8000

## 2. Create a Webpage and Simple Map

We will start from scratch to build a web map, with a tile base layer, some mapped data, and some basic interactivity.

![](img/polygon.png)

### 2.1 Create a working directory

Our first step is create a working directory. This directory stores all of the files associated with our specific web page and web map. Next, please activate a web server as described in **section 1.3**.

If you don't have access to a web directory or server, you can set up a local development environment that mimics a web server on your own machine. This is called a **localhost server**. In this exercise, a simple Python localhost server will do.

### 2.2 Setup a web page for our map

Open up your IDE, and then we set up an empty **index.html** template for our web page that will contain our web map and web map elements. The components will be the same as always, note the head, title, and body.

Enter the following code into your blank HTML page.

```html
<!DOCTYPE html>
<html>
<head>
    <title>Leaflet Map</title>
</head>
<body>
    <!-- Our web map and content will go here -->
</body>
</html>
```
From here, we will do the following four things to add a map to our page:

- Reference the Leaflet CSS and JavaScript files;
- Add a div element to our page that will hold the map;
- Create a map object in Javascript that will interact with the map div element; and
- Add the tiled OpenStreetMap basemap to our map object using tileLayer.

### 2.3 Reference the Leaflet CSS and JavaScript files

We need to load Leaflet into our web page before we can start using the library. There are two options for doing this, we can download the library files from the Leaflet download site, or we can use the hosted version.

>  We are not planning on changing the JavaScript or the CSS, so it is easiest to use the hosted libraries. Reference these in your HTML by adding the following lines of code.

Within the head section, after title, copy and paste the following. This adds the Leaflet CSS file to our web page and includes Leaflet styles.

```html
<!-- External Stylesheets -->
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.0.2/dist/leaflet.css" />
```

Link to the JavaScript library at the bottom of the body section of our site, putting it at the bottom allows our page to load faster. Copy and paste the following. This adds the Leaflet JS file to our web page and is the Leaflet Javascript library.

```html
<!-- Add the Leaflet JavaScript library -->
<script src="https://unpkg.com/leaflet@1.0.2/dist/leaflet.js"></script>
```

We can now begin working with the Leaflet library.

### 2.4  Add a map div

Add a div to the body that will hold the map. This is just like any other div element we might use. We will set the style right in the div using the style attribute, and not the CSS file, otherwise all map divs we create will have the same styling.

```html
<div id="map" style="width: 900px; height: 600px"></div>
```

### 2.5 Use Javascript to create the map object

Now we can start coding the map using JavaScript. The Leaflet library is referenced by using L. followed by the class. The first step is to create the map object using the map class. Set the variable map to be our Leaflet map object. More reading on L.map can be found in the extensive Leaflet documentation. Set the center of the map to be at the Memorial Union Quad  `(44.56576, -123.27888)` and zoom level to `14`. Enter the following in our document at the end of the body section.

```html
<script>
    // Create variable to hold map element, give initial settings to map
    var map = L.map('map',{ center: [44.56576, -123.27888], zoom: 16});
</script>
```

> **Note:**
>
> - the script tags, this is where we will will put all of our JavaScript for the map.
> - Where did I get my Lat/Lon values? **A nice trick is to find the locations by navigating to [Google Maps](http://maps.google.com)**, right clicking on a location on the map, and selecting 'What's here?'. This will provide latitude and longitude values for that location you can then copy.

### 2.6 Add a tiled basemap with tileLayer

The last step in getting a basic map running is add a layer. We are going to use what is called a tile layer, which is a fundamental technology behind many web maps. There are many tile layers you can add to your maps. The one we are going to use today is from OpenStreetMap. To add a tile layer to the map, we use the L.tileLayer class. Place the following code within your script tags.

```javascript
// Add OpenStreetMap tile layer to map element
L.tileLayer('http://{s}.tile.osm.org/{z}/{x}/{y}.png', { attribution: '&copy; OpenStreetMap' }).addTo(map);
```

> Note the attribution. Here we can provide reference for the source of the base map, and any other attribution for map elements we want to provide. It will appear in the lower right corner of our map by default, but you can change this. Read more about attribution here.

**Our Basic Map**

Save your HTML document and open your web browser to your localhost server (http://localhost:8000). You will see the map we just created!

![](img/basemap.png)

**Additional Tile Layers**

There are a number of resources that have tile layers you can use with Leaflet JS. An excellent resource for examining and previewing tile layers is called Leaflet Provider. Scan [through available tile layers and preview them](http://leaflet-extras.github.io/leaflet-providers/preview/), and try replacing the L.tileLayer with one of the other tile layers in your code.

![](img/layer_preview.png)

## 3. Add Individual Data to our Map

To introduce adding data, we will learn how to add markers, polylines, and polygons to our map. There are multiple methods for adding data, including methods in which you can add large datasets.  This section will show how you can simple points, polylines, and polygons to your map.

### 3.1 Adding Points (aka Markers)

To add a point to your map, we use the `L.marker` class. To add a point, we specify a latitude and longitude, then add the marker to our map. Enter the following line of code in the script block in the body section of the document, following the tile layer.

```js
// Create point feature for Wilkinson Hall
var myDataPoint = L.marker([44.56822, -123.28034]).addTo(map);
```

![](img/marker.png)

### 3.2 Adding Polylines

To add a polyline (a line that can have multiple segments) to your map, we use the `L.polyline` class. Just like with the marker, we use latitude and longitude to add the line vertices. An important difference however, is that we need to add a color and weight, if we don't add a weight you won't be able to see the line. You can set style options in brackets after the array of line vertices.

>  **NOTE:** the polyline is formed by an array, and draws in that order. Enter the following into our script.

```js
// Create line feature for the Route from Wilkinson Hall to Strand Ag Hall, style and add to map
var myDataLine = L.polyline([[44.5656915, -123.2775289], [44.5656992, -123.2778923], [44.5662266, -123.2778722], [44.5682559, -123.2778293], [44.5682445, -123.2800823]],
    {color: 'red', weight: 5}).addTo(map);
```
![](img/polyline.png)


### 2.3 Adding Polygons

Adding polygons is very similar, we use the L.polygon class. Specify a latitude and longitude for each node, then add to our map. Set the style just the same. Enter the following in our script.

```js
// Create area feature for Strand Ag Hall, style and add to map
var myArea = L.polygon([[44.5651985, -123.2769978],[44.566131, -123.2769978], [44.5661339, -123.2775027], [44.5651985, -123.2775182], [44.5651985, -123.2769978],],
    {color: 'orange', weight: 5}).addTo(map);
```
Save your document and refresh your browser.

![](img/polygon.png)

### 3.4 Other Simple Vector Data Types

There are a number of other simple data types and groups you can add, read more about them in the Leaflet documentation. These include:

- [Path](http://leafletjs.com/reference.html#path)
- [MultiPolyline](http://leafletjs.com/reference.html#multipolyline)
- [MultiPolygon](http://leafletjs.com/reference.html#multipolygon)
- [Rectangle](http://leafletjs.com/reference.html#rectangle)
- [Circle](http://leafletjs.com/reference.html#circle)
- [CircleMarker](http://leafletjs.com/reference.html#circlemarker)

### 3.5 Feature Groups and GeoJSON

Leaflet also supports adding groups of features using class called [L.featureGroup](http://leafletjs.com/reference.html#featuregroup). If we wanted, we could have restructured our code to the point, line, and polygon above by placing them all in a feature group.

Additionally, Leaflet is designed work natively with GeoJson. We will look at how to get GeoJson to a Leaflet Map later.


## 4. Add Interactivity with Pop ups

Leaflet makes it easy to add pop ups to your place markers (points). Pop ups are a simple way to add interactivity to your map. When a viewer clicks on the pop up, information will be displayed. Pop ups are included by binding them to the marker or feature that you wish to apply a pop up on. When the visitor clicks on this feature, the bound pop up will appear.

### 4.1 Add a pop up to our marker layer

There is a marker sitting on our map at Wilkinson Hall. Let's add a popup that tells us this is Wilkinson Hall. The simplest way to add a pop up is to use the bindPopup method of `L.marker`. Enter the following code snippet in your script block in your HTML document, and we will step through what is happening.

```js
// Bind popup to Data Point object
myDataPoint.bindPopup("This is Wilkinson Hall.");
```

Save and refresh your map. Click on the marker. You will see a pop up stating "This is Wikonson Hall." appear. bindPopup is 'method' of our marker object class, just like `addTo('map')` we used above. Methods are actions that can be performed on objects, and marker is an object. Also note, within the quotations where we wrote "This is Wilkinson Hall.", we can write HTML as content. Change the code to the following, and see what happens.

```js
// Bind popup to data point object
myDataPoint.bindPopup("<h3>Wilkinson Hall</h3><p>Corvallis, Oregon<br>College of Earth, Ocean, and Atmostpheric Sciences</p>");
```

![](img/html_popup.png)

This means, within our popup, we can add links, images, lists, and many other HTML elements. This can also include pictures like what we have done in practical exercise 1. Also, we can even include videos, tweets, and etc.

> **Question:** How can we add a YouTube clip to the pop-up info windows?

### 4.2 Add pop ups to our other data features

Just like with the marker object, we can add pop ups to our other features using the bindPopup method. Use the variable that we set the feature to (e.g., `var = myDataPoint; var = myDataLine; and var = myArea;`) as the object, then use `bindPopup`. Enter the following block of code in your script tags, after the other code.

```js
// Bind popup to line object
myDataLine.bindPopup("The route from Wilkinson Hall to Strand Ag Hall.");
// Bind popup to area object
myArea.bindPopup("Strand Ag Hall");
```

Save and refresh. Click on the data features to see the pop ups in action.

## 5. Map Events

What the map does when a user interacts with it and its various components is called an Event. A pop up is a very basic built-in event, but there are many other events that Leaflet can handle. The main one we will focus on here is what happens when a visitor clicks on the map, or what happens when there is a "Mouse Event". When a visitor clicks on the map, you can return a handful of different properties. One of them is latitude and longitude, making it easy to add simple functionality that will return latitude and longitude of the location where the mouse was clicked.

### 5.1 Find Latitude and Longitude of a Mouse Click

To complete that task, we need to do a couple of things.

1. Add an empty pop up object to our map.
2. Write a function that creates a pop up.
3. Tell the map that when it is clicked, run this function.

The following snippet of code does just that. Read through it and see how it addresses each step. Enter this into document in between the script tags.

```js
// Create an Empty Popup
var popup = L.popup();

// Write function to set Properties of the Popup
function onMapClick(e) {
    popup
        .setLatLng(e.latlng)
        .setContent("You clicked the map at " + e.latlng.toString())
        .openOn(map);
}

// Listen for a click event on the Map element
map.on('click', onMapClick);
```

Let's break this down a bit. First we created our empty pop up object using `L.popup()`. The next part is a JavaScript function. A JavaScript function is a block of code designed to perform a particular task and is executed when calls it.

![](img/click_on_map.png)

### 5.2 More information on Javascript functions.

In this case, the function changes the properties of the pop up, or in our case, sets them, because the pop up object is empty. It **(a)** sets the lat and lng of the pop up to the location of the mouse click, **(b)** sets the content of the popup to say what that location is (has to convert it to a string to do so), and then **(c)** opens the popup on the map. Finally, the last piece, is an event on the map object that says on click, run the function onMapClick. Complex, yet surprisingly simple all at once.

Save and refresh. Click on the data features to see the pop ups in action.

More on events is found in the [Leaflet documentation](http://leafletjs.com/reference.html), under each object, look at the events and properties that are available for you to utilize and manipulate.

## 6. Add a GeoJSON

Learning the fundamentals of adding small datasets to our map along with some basic interactivity is important, but often times you will be adding larger datasets to our maps, sometimes containing hundreds of features. Leaflet is designed to work natively with a data format called GeoJSON. GeoJSON is JavaScript object that contains geographic data. This might not make sense right now, and that is fine, we will discuss JavaScript in depth in the next session. But for now, lets look at one way to load a GeoJSON into our map.

**The GeoJSON**

The assets directory contains a file called **"geog371.geojson"**. This is a dataset of several geographic features containing the lecture, lab, and office hour location of the course Geography 371, and the route linking the lecture and lab location to the office hour location.  Open up the GeoJSON in Webstorm or other IDEs to see what a GeoJSON looks like. Also, you open this geojson file by a web application at http://www.geojson.io.  As shown below.

![](img/geojsonio.png)

### 6.1 Use the JQuery JavaScript Library

The first thing is add a leaflet plugin called `leaflet.ajax.min.js` to our page.  This plugin makes it easy to manipulate a web page by finding elements on the page, setting their styles and properties, handling interaction events, and more. It has a nice helper method `L.geoJson.ajax()`, we will use it to load our GeoJSON file onto our map.

Enter the following line of code at the bottom of the body section to add the leaflet.ajax method to our page after the lines that add the Leaflet JavaScript library.

```html
<body>
    ...
        <!-- HTML Page Elements are here -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/leaflet-ajax/2.1.0/leaflet.ajax.min.js"></script>
        <!-- Web Map Scripts are here -->
    ...
</body>
```

### 6.2 Add the GeoJSON

 Within the brackets, we put the location of the GeoJSON on our server `assets/geog371.geojson`.

To add the GeoJSON to the map, use [L.geoJson()](http://leafletjs.com/reference.html#geojson) the Leaflet library. Pass the dataset to `L.geoJson`, then add it to the map element. Simple enough right?

Add the following code to your `script`, between the script tags.

```js
    // load GeoJSON from an external file
    L.geoJson.ajax("assets/geog371.geojson",{
        // add GeoJSON layer to the map once the file is loaded
    }).addTo(map);
```

Simple enough right? Click save and refresh your page to see the GeoJSON added to the map.

![](img/geojson_loaded.png)

### 6.3 Add Popups to Show the feature name

We can see the points, but they might not be very useful without adding popups. We can add popups in a very similar manner as above, except since we are using a full dataset, it doesn't make much sense to add them one by one. The `L.geoJson` object has a option called `onEachFeature` that runs a function on each feature when it is added to the map. We can use this to run a function that adds a popup to each feature when it is added to the map. The syntax, which goes in brackets after we specify the data we are adding, looks like the following. Enter this into your `getJSON` and `L.geoJson` functions.

```js
// load GeoJSON from an external file
    L.geoJson.ajax("assets/geog371.geojson",{
        onEachFeature: function (feature, layer) {
            layer.bindPopup(feature.properties.name);
        }
    }).addTo(map);
```

Once entered, save and refresh your page. Click on one of the popups, you will see the name of the feature appear.

![](img/popup.png)


##  7. Concluding remarks

To wrap up, lets leave it here for this lesson. We covered the majority of fundamentals for creating, adding data, and displaying a Leaflet map. Continue to explore [the documentation on the Leaflet site](http://leafletjs.com/reference.html) to see what you can do with the various elements of the map we worked on in this session.


## References:

[1] I was highly inspired by the lecture material from  http://duspviz.mit.edu/web-map-workshop/leaflet-js/