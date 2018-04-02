# Practical Exercise Two: Base Map Design

> Spring 2017 | Geography 472/572 | Geovisualization: Geovisual Analytics
>
> Instructor: Bo Zhao | TA: Kyle R. Hogrefe | Location: Wilkinson 235 | Time: Tuesday 18-19:50pm
>
> Assigned: 05/02/2017 | Due: 05/16/2017 @11:59pm | Points Available = 50

This Practical Exercise will help you publish a base map using Mapbox.  Mapbox is a large provider of custom [online maps](https://en.wikipedia.org/wiki/Online_maps) for websites such as [Foursquare](https://en.wikipedia.org/wiki/Foursquare), [Pinterest](https://en.wikipedia.org/wiki/Pinterest), [Evernote](https://en.wikipedia.org/wiki/Evernote), the Financial Times, [The Weather Channel](https://en.wikipedia.org/wiki/The_Weather_Channel) and [Uber Technologies](https://en.wikipedia.org/wiki/Uber_Technologies).Since 2010, it has rapidly expanded the niche of custom maps, as a response to the limited choice offered by map providers such as [Google Maps](https://en.wikipedia.org/wiki/Google_Maps) and [OpenStreetMap](https://en.wikipedia.org/wiki/OpenStreetMap). Mapbox is the creator of, or a significant contributor to some open source mapping libraries and applications, including the MBTiles specification, the TileMill cartography IDE, the [Leaflet](https://en.wikipedia.org/wiki/Leaflet_(software)) JavaScript library, and the CartoCSS map styling language and parser.The data are taken both from open data sources, such as [OpenStreetMap](https://en.wikipedia.org/wiki/OpenStreetMap) and [NASA](https://en.wikipedia.org/wiki/NASA), and from proprietary data sources, such as [Digital Globe](https://en.wikipedia.org/wiki/DigitalGlobe).

## 1. Warm-up

To learn how to create a base map via Mapbox, you need to read a tutorial on [How to Create a Custom Style](https://www.mapbox.com/help/create-a-custom-style/).  This tutorial will walk through creating a custom style in the **Mapbox Studio style editor**. You’ll start with a list of colors pulled from the Mapbox logo, and apply them to the Mapbox Basic style. In the end, you’ll have created a custom-branded map style that reflects the Mapbox brand at any zoom level and at any place across the world.

If you have other complicated troubles in making maps via MapBox, please check the [Design a Map Section of the Mapbox Tutorial](https://www.mapbox.com/help/#design-a-map).

## 2. Publish your MapBox basemap

Once you’ve finished adding data and styling your map, the next step is to add it to a web page. This section covers everything you can do with your published style. Please read the tutorial [Publish Your Style](https://www.mapbox.com/help/studio-manual-publish/).

To use your map style with **Leaflet**, you will need the **style URL** for your map and an **access token** associated with your account. 

### 2.1 Style URL

A [style URL](https://www.mapbox.com/help/define-style-url/) is how you refer to your map style in other Mapbox tools. Combined with your access token, it allows you to access and use your map with any of the [Mapbox developer tools](https://www.mapbox.com/developers).

A complete style URL is made up of three components:

```
mapbox://styles/mapbox/streets-v9
```

- `mapbox://styles` – points to Mapbox’s styles API
- `/mapbox` – your Mapbox username
- `/streets-v9` – your style’s unique ID

You can find your map’s style URL in the [Mapbox Studio interface](https://www.mapbox.com/help/studio-manual-interface/).

>**Note:** The mapbox://styles notation for Mapbox styles is an alias to the full Styles API URL: https://api.mapbox.com/styles/v1/streets-v9.

### 2.2 Access Token

Mapbox uses **access tokens** to associate your apps and tool usage with your account. Every account has a default public access token, but you can create new access tokens as well. Your default access token is listed on your Mapbox Studio home page. You can also [manage your access tokens](https://www.mapbox.com/studio/account/tokens/) with Mapbox Studio. 

![](img/mapbox-style-share.png)

> The web interface of https://www.mapbox.com/studio/styles/

### 2.3 Use the customized basemap in leaflet

In order to show how to use a customized basemap in leaflet, please refer to the source codes in the lecture material at the [wk05/wk05_2__lab04]( wk05/wk05_2__lab04). Below are the major steps.

1\. By clicking on the **Share, develop & use** item, you will be directed to a new page. In the **develop with this style** section, you can find the access token. 

2\. Download the zipped style package by pressing the download item. To use the style package, please unzip it to the **assets** subdirectory of your working folder. You will find a `style.json` file in the folder. You will need to include this json in your html file.

3\. To use a customized basemap, we should include two major libraries except leaflet. 

```javascript
<!-- Stylesheet -->
<link rel="stylesheet" href="http://cdn.leafletjs.com/leaflet/v1.0.3/leaflet.css" />
<link href="https://api.tiles.mapbox.com/mapbox-gl-js/v0.35.1/mapbox-gl.css" rel='stylesheet' />
<!-- Javascript Libraries -->
<script src="http://cdn.leafletjs.com/leaflet/v1.0.3/leaflet.js"></script>
<!-- mapbox gl js -->
<script src="https://api.tiles.mapbox.com/mapbox-gl-js/v0.35.1/mapbox-gl.js"></script>
<!-- leaflet mapbox js -->
<script src="http://rawgit.com/mapbox/mapbox-gl-leaflet/master/leaflet-mapbox-gl.js"></script>
```

4\. Use a customized MapBox layer.

```javascript
var gl = L.mapboxGL({
  accessToken: 'pk.eyJ1Ijoiemhhb2JvIiwiYSI6ImNqMGdpM2RjNDAyMzQzMnJ1d3FuZmF0NnQifQ.yoQP0NDS5F8ePKjaS3EJgQ',
  style: 'assets/style.json'
}).addTo(map);
```

To learn the [full code](index.html), please refer to the lab material. The following map will be shown once I execute the `index.html` file.

![](img/customized-style-brown.png)

## 3. On the shoulders of giants

You can learn from other popular map design styles, Here are a list of base map you may feel useful. However, **Notably, learning from a map style is NOT exactly copying a map style. We expect to see your own contribution. **

**OSM Previews**

Please locate and switch to a variety of styles on the right scrollable panel.

![](img/osm_preview.png)

**MapBox**

![](img/mapbox.png)

**[MapZen Tangram Play](https://mapzen.com/tangram/play/)**

![](img/mapzen.png)

**Google My Maps**

![](img/google-my-maps.png)



To capture the color of a map, you can follow the following procedure. 

- Create a screenshot of a map;

- Paste the screenshot to one slide in `Microsoft Powerpoint`;

- Click the `eyedropper` tool under the `Format` tab.

  ![](img/ppt.png)

- In `Picture Border` dropdown list, you can get the RGB value of the color by clicking the `more color` item.

  ![](img/color.png)



- based on a RGB to Hex color conversion tool at [http://www.rapidtables.com/convert/color/rgb-to-hex.htm](http://www.rapidtables.com/convert/color/rgb-to-hex.htm).

![](img/RGB_to_Hex_color_converter.png)



## 4. Deliverable

With the help of mapbox, you are expected to make at least two base maps. You can design these two base maps for your group project or design base maps for something of your interests.  I encourage you start from a mapfox featured style, such as the Mapbox Street, Oudoors, Dark, Light and etc.

![](img/mapbox-featured-styles.png)

While designing the base map, you are expected to practice what you have learned during the lectures, such as symbolization, color, layout, labelling, typography and etc. Also, **Make sure you design a base map rather than a thematic map**. The base map is created for illustrating the contextual information of a geovisualization as well as for standing out the thematic features.


To submit this practical exercise, you will need to create a GitHub repository.  The file structure of your GitHub repository should look like:

```Powershell
GEOG4572-PE2
│readme.md
│map1.html
│map2.html
├─css
│      style.css
├─img
└─js
        main.js
```

This repository should contain the following items:

- Two html files, each of which shows a base map you have designed via MapBox. (**30 POINTS IN TOTAL, 15 FOR EACH**)
- A readme.md contains:
  - The titles of the basemaps;  (**3 POINTS**) 
  - A short descriptions of the basemaps;  (**5 POINTS**) 
  - Two rawgit.com url links, each of which directs you to a base map ; and  (**5 POINTS**) 
  - Please talk about what specific idea motivates you to design the two maps? For example, you can design a map driven by a LGBT topic (I guess the geometric features on the map will be in a rainbow color ramp), or driven by the idea of Beaver Nation (Orange and Black?), Christmas season or Saint Patrick's Day.  (**7 POINTS**) 

Once you finish this practical exercise, please upload the repository of your web map to GitHub, and **only submit the url of the repository to canvas**. Please contact the instructor or TA if you have any difficulty in submitting the url.