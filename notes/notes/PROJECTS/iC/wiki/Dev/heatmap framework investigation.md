Investigation of available frameworks for web browser heatmap visualization.
Criteria: visuals, license, price, deployment, server load, docker? data format...


## heatmap.js
[web](https://www.patrick-wied.at/static/heatmapjs/), [github](https://github.com/pa7/heatmap.js), [docs](https://www.patrick-wied.at/static/heatmapjs/docs.html) [animated example](https://www.patrick-wied.at/static/heatmapjs/example-heatmap-animation.html)
Deployment: eazy, just install a package, then run webserver
MIT license
```javascript
var dataPoint = {
  x: 5, // x coordinate of the datapoint, a number
  y: 5, // y coordinate of the datapoint, a number
  value: 100 // the value at datapoint(x, y)
};
var dataPoints = [dataPoint, dataPoint, dataPoint, dataPoint];
heatmapInstance.addData(dataPoints);
```
Then you can specify colors, radius, opacity, upper, lower bounds.
Then it is possible to get data, re-draw, update, change in time?
Rendering took 53ms

## D3
[web](https://d3js.org/)[docs](https://d3js.org/getting-started) [github](https://github.com/d3)
opensource - ISC License
Tool for web visualisations, many other options available
[contours example](https://observablehq.com/@d3/contours?intent=fork)
Generates svg, then you can download as svg, png...
[heatmap](https://d3-graph-gallery.com/heatmap.html), [density](https://d3-graph-gallery.com/graph/density2d_shading.html), [histogram](https://d3-graph-gallery.com/graph/density2d_histogram2d.html)


## LightningChart
[web](https://lightningchart.com/js-charts/)[performance](https://github.com/Arction/javascript-charts-performance-comparison-heatmaps)

They claim to be the fastest of all js competitors. Visuals not as nice. 2500 USD
Defined with intensity matrix.
```js
// Example syntax, invalidate intensity values override #1, specify data from beginning of heatmap.
heatmap.invalidateIntensityValues([
    // dataOrder: 'columns', columns: 3, rows: 5
    [0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0],
])
```

## plotly
https://plotly.com/javascript/2d-density-plots/
opensource, has other applications, is interactive
## mapbox
https://docs.mapbox.com/mapbox-gl-js/example/heatmap-layer/
Probably not really relevant
## Polymaps
[web](http://polymaps.org/)[github](https://github.com/simplegeo/polymaps)
Free, not as nice as others

# ZingChart
[web](https://www.zingchart.com/) [example](https://www.zingchart.com/gallery/radar-chart-heatmap), [pricing](https://www.zingchart.com/pricing)
99 USD/year
API is nice

# EChart
[web](https://echarts.apache.org/en/index.html)[example](https://echarts.apache.org/examples/en/editor.html?c=heatmap-large)[license](https://github.com/apache/echarts/blob/master/LICENSE)[github](https://github.com/apache/echarts)
Free, seems nice, API ok
with background?


_Highchart, ZingChart, EChart_