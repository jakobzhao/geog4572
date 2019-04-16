# DC.js Fundamentals

> Spring 2018 | Geography 4/572 | Geovisualization: Geovisual Analytics
>
> **Instructor:** Bo Zhao  **Location:** WITH 205 | **Time:** TR 1100 - 1150

**Learning Objectives**

- Understand the fundamental concepts, functions of DC.js; and
- Able to draw a chart using Dc.js.

`dc.js` is a JavaScript Library that allow you to develop graphs/charts, and highly interactive Dashboards. `dc.js` builds on `d3.js` and use `d3.js` to render charts in CSS friendly SVG format. By using this library you will be able to develop bar chart (histogram), pie chart, row chart, line chart, bubble chart, geo choropleth chart, and others. You can link the charts to each other to make a well connected charting interface for your work.

This JavaScript library is really a powerful tool for data visualization and analysis on the web. Here in this tutorial we'll try to cover some basics of `dc.js` that will help you to move on with `dc.js`.

>  **note:** dc.js didn't works alone, it require `crossfilter.js` and `d3.js` to work.

1\. [crossfilter](https://github.com/square/crossfilter/wiki) is also a JavaScript library released by Square, allow you to explore large multidimensional datasets. It aggregates and filter raw data extremely fast (<30ms). It doesn't have its own user interface, so it combine to work with `d3.js` and Google Visualization API. It’s really easy to get your raw data into `crossfilter.js` by using JSON data format.

2\. [D3](https://d3js.org/) also known as Data-Driven Documents or `d3.js`, a JavaScript Library for data visualization, allow you to present raw data into a more visual form using SVG, Canvas and HTML5 and CSS standards. It is the more powerful library of JavaScript as to visualize data in graphical format as compared to above mentioned.

Please copy the following libraries in the same order to your html file. Besides, make sure you include the css stylesheet for `dc.css`.

```html
<link rel="stylesheet" type="text/css" href="http://dc-js.github.io/dc.js/css/dc.css"/>
<script type="text/javascript" src="https://d3js.org/d3.v5.min.js"></script>
<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/crossfilter/1.3.12/crossfilter.min.js"></script>
<script type="text/javascript" src="https://dc-js.github.io/dc.js/js/dc.js"></script>
```

Now, we are able to work with dc.js, So, lets start. Let us try to build a bar chart.

To develop any chart you need some raw data, for which you want to build a chart. it should be in JSON or cvs format. Here in the following example we use a json data, which is stored in `assets/payments.json`.

**The data: `payments.json`**

```json
[
  {"date": "2011-11-14T16:17:54Z", "quantity": 2, "total": 190, "tip": 100, "type": "tab"},
  {"date": "2011-11-14T16:20:19Z", "quantity": 2, "total": 190, "tip": 100, "type": "tab"},
  {"date": "2011-11-14T16:28:54Z", "quantity": 1, "total": 300, "tip": 200, "type": "visa"},
  {"date": "2011-11-14T16:30:43Z", "quantity": 2, "total": 90, "tip": 0, "type": "tab"},
  {"date": "2011-11-14T16:48:46Z", "quantity": 2, "total": 90, "tip": 0, "type": "tab"},
  {"date": "2011-11-14T16:53:41Z", "quantity": 2, "total": 90, "tip": 0, "type": "tab"},
  {"date": "2011-11-14T16:54:06Z", "quantity": 1, "total": 100, "tip": 0, "type": "cash"},
  {"date": "2011-11-14T16:58:03Z", "quantity": 2, "total": 90, "tip": 0, "type": "tab"},
  {"date": "2011-11-14T17:07:21Z", "quantity": 2, "total": 90, "tip": 0, "type": "tab"},
  {"date": "2011-11-14T17:22:59Z", "quantity": 2, "total": 90, "tip": 0, "type": "tab"},
  {"date": "2011-11-14T17:25:45Z", "quantity": 2, "total": 200, "tip": 0, "type": "cash"},
  {"date": "2011-11-14T17:29:52Z", "quantity": 1, "total": 200, "tip": 100, "type": "visa"}
]
```

**The web page: `index.html`**

```html
<!DOCTYPE html>
<html>

<head>
    <title>DC.js Bar Chart</title>
    <link rel="stylesheet" type="text/css" href="http://dc-js.github.io/dc.js/css/dc.css" />
    <script type="text/javascript" src="https://d3js.org/d3.v5.min.js"></script>
    <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/crossfilter/1.3.12/crossfilter.min.js"></script>
    <script type="text/javascript" src="https://dc-js.github.io/dc.js/js/dc.js"></script>
</head>

<body>
<div id="barChart"></div>

<script type="text/javascript">
    d3.json("assets/payments.json").then(function(data) {
        ...
        ...
        ...
    });

</script>
</body>

</html>

```

After that feed this data to crossfilter object to process this data.

`var facts = crossfilter(data);` we named it as facts, each row in JSON data called fact.

You can also check this data in the console writing this line `console.log(facts);`

> **Note:** More details about crossfilter functions, please look at Peter Cook (201X) Getting to know Crossfilter http://animateddata.co.uk/articles/crossfilter/

Now we'll have to create a dimension of our data, It means, if you want to know how many total payments you've made, for this we need to create a dimension. You can create any dimension of your data.

```javascript
var dimensionByTotal = facts.dimension(function (d){ return d.total;});
```

Then we grouped our data with the help of dimension we just created. It means if you want to know how many payments are done of the each amount (how many $100 payments). As you can see in our data there are six $90 payment and two $200 and so on. To group our data, here is the statement.

```javascript
var groupByTotal = dimensionByTotal.group(function(d){ return Math.floor(d/100)*100; });
```

Here "dimensionByTotal " is the variable we just created to generate dimension.

All we have done our data related stuff, now we will move to build a bar chart. For this create an object of bar chart.

```javascript
var barChart = dc.barChart("#chart")
```

`#barChart` is the ID of the `div` in which we want to show our data.

```javascript
        var barChart = dc.barChart('#barChart')
            .width(1024) // width of the chart
            .height(200) // height of the chart
            .dimension(dimensionByTotal) // dimension we create before passed as parameter
            .group(groupByTotal) // group we created before passed as parameter to barChart method
            .x(d3.scaleLinear().domain([0, 400])) // created x-axis scales
            .xUnits(dc.units.fp.precision(100)); // it defines the units of x-axis
            // .x(d3.scaleOrdinal())
            // .xUnits(dc.units.ordinal);
        barChart.yAxis().ticks(5);
        barChart.xAxis().ticks(4);
        dc.renderAll();
```

![](img/bar1.png)


**Ordinal Bar Chart**

Bar charts that display the data that are classified into nominal or ordinal categories, such as in our raw data if we want to classified our data by Type, there are three types of data in our raw data, visa, tab, cash. If we develop a bar chart on type dimension the bar chart is called Odinal-Bar Chart.

To create ordinal bar chart just replace this code with specific methods in the code.

Total dimention with Type Dimension

`var dimensionByType = facts.dimension(function (d){ return d.type;});`

and Dimension Group with this new code

`var groupByType = dimensionByType.group().reduceCount(function(d){ return d.type; });` reduceCount function counts the total number of records.

Then change the dimension and group variable from barCharts methods.

`.dimension(dimensionByType)`

`.group(groupByType)`

Change the x-axis scale and units to ordinal

`.x(d3.scaleOrdinal())`

`.xUnits(dc.units.ordinal)`

Thats it, you see how it is easy to create charts with dc.js

![](img/bar2.png)


## References

[1] [https://utopian.io/utopian-io/@faad/tutorial-1-dive-into-dc-js-a-javascript-library-bar-chart](https://utopian.io/utopian-io/@faad/tutorial-1-dive-into-dc-js-a-javascript-library-bar-chart)

[2] Dc.js examples

- [Area Chart](http://dc-js.github.io/dc.js/examples/area.html)

- [Bar Chart](http://dc-js.github.io/dc.js/examples/bar.html)

- [Line Chart](http://dc-js.github.io/dc.js/examples/line.html)
