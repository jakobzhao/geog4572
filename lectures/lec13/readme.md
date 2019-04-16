# Heatmap

> Spring 2019 | Geography 4/572 | Geovisual Analytics
>
> **Instructor:** Bo Zhao  **Location:** Wilkinson 210 | **Time:** TR 1600 - 1650

**Learning Objectives**

- make a heat map of points.


![](img/leaflet.heat.png)

Leaflet.heat is a tiny, simple and fast [Leaflet](http://leafletjs.com) heatmap plugin.

**Demos**

- [10,000 points ](http://leaflet.github.io/Leaflet.heat/demo)
- [Adding points dynamically ](http://leaflet.github.io/Leaflet.heat/demo/draw.html)

### 1 Usage

```js
var heat = L.heatLayer([
	[50.5, 30.5, 0.2], // lat, lng, intensity
	[50.6, 30.4, 0.5],
	...
], {radius: 25}).addTo(map);
```

To include the plugin, just use `leaflet-heat.js` from the `dist` folder:

```html
<script src="leaflet-heat.js"></script>
```

### 2 L.heatLayer(latlngs, options)

Constructs a heatmap layer given an array of points and an object with the following options:
- **minOpacity** - the minimum opacity the heat will start at
- **maxZoom** - zoom level where the points reach maximum intensity (as intensity scales with zoom),
  equals `maxZoom` of the map by default
- **max** - maximum point intensity, `1.0` by default
- **radius** - radius of each "point" of the heatmap, `25` by default
- **blur** - amount of blur, `15` by default
- **gradient** - color gradient config, e.g. `{0.4: 'blue', 0.65: 'lime', 1: 'red'}`

Each point in the input array can be either an array like `[50.5, 30.5, 0.5]`,
or a [Leaflet LatLng object](http://leafletjs.com/reference.html#latlng).

Optional third argument in each `LatLng` point (`altitude`) represents point intensity.
Unless `max` option is specified, intensity should range between `0.0` and `1.0`.

### 3 Methods

- **setOptions(options)**: Sets new heatmap options and redraws it.
- **addLatLng(latlng)**: Adds a new point to the heatmap and redraws it.
- **setLatLngs(latlngs)**: Resets heatmap data and redraws it.
- **redraw()**: Redraws the heatmap.


Using this Heatmap plugin for leaflet, I created a heatmap of cell towers in Oregon. Please pay attention to how to link in the **leaflet heat plugin**, and how to use the **heatlayer**.

### 4 Heatmap generation

```HTML
<!DOCTYPE html>
<html>
<head>
  <title>Cell Tower Heat Map </title>
  <link rel="stylesheet"  href="http://cdn.leafletjs.com/leaflet-0.7/leaflet.css" />
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.0.2/dist/leaflet.css" />
  <script src="https://unpkg.com/leaflet@1.0.2/dist/leaflet.js"></script>
  <script src="http://leaflet.github.io/Leaflet.heat/dist/leaflet-heat.js"></script>
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.0/jquery.min.js"></script>
</head>
<body>
	<div id="map" style="width: 900px; height: 600px"></div>
<script src="assets/2013-earthquake.js"></script>
<script>
	var map = L.map('map').setView([44.1, -120.5], 7);
	L.tileLayer( 'http://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
		attribution: '&copy; \<a href="http://openstreetmap.org"\>OpenStreetMap\</a\> Contributors',
		maxZoom: 18
    }).addTo(map);

	var heat = null;
	// Get GeoJSON and put on it on the map when it loads
	$.getJSON("assets/cell_towers.geojson",function(data){
      // set cellTowers to the dataset, and add the cell towers GeoJSON layer to the map
      cell_tower_data = [];
      for (var i = 0; i < data.features.length; i++ ) {
          cell_tower_data[i] = [
                      data.features[i].geometry.coordinates[0][1],
                      data.features[i].geometry.coordinates[0][0]]
      }

      heat = L.heatLayer(cell_tower_data,{
            radius: 35,
            blur: 10,
            maxZoom: 17,
            gradient: {0.05: 'blue', 0.25: 'lime',  0.27: 'yellow', 0.3: 'red'}
          }).addTo(map);
	});

</script>
</body>
</html>
```

![](img/heatmap-client.png)
> using leaflet.heat to create a heat map at the client side.
