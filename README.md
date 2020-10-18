# Usage from cdn

Add this to HTML head (loads dependencies)

    <script src="https://cdn.jsdelivr.net/gh/epiviz/epiviz-chart/cdn/jquery/dist/jquery.js"></script>
    <script src="https://cdn.jsdelivr.net/gh/epiviz/epiviz-chart/cdn/jquery-ui/jquery-ui.js"></script>
    <script src="https://cdn.jsdelivr.net/gh/epiviz/epiviz-chart/cdn/renderingQueues/renderingQueue.js"></script>
    <script src="https://cdn.jsdelivr.net/gh/epiviz/epiviz-chart/cdn/webcomponentsjs/webcomponents-lite.js"></script>

    <link rel="import" href="https://cdn.jsdelivr.net/gh/epiviz/epiviz-chart/cdn/epiviz-components.html">

# Installation from source

`bower install epiviz/epiviz-chart`

# Documentation

run a local instance of polymer-server
`polymer serve`

Then navigate to http://localhost:8080/components/epiviz-chart/

# Demo

run a local instance of polymer-server
`polymer serve`

Then navigate to http://localhost:8080/components/epiviz-chart/demo/


# Update chartSettings:

```
# get chart
chart = document.querySelector("#chart1");
# get current chart settings
currentSettings = chart.ChartSettings;
# modify chart settings
...

# set settings back to chart
chart.setAttribute("chart-settings", JSON.stringify(currentSettings));
```

# Epiviz-environment

### must use polymer api to add charts to environment. Js dom api does not properly initialize elements

for example

if the page contains

```
<epiviz-environment id="env">
</epiviz-environment>
```

to add an epiviz chart for example line-track.

# create a new element
```
elem = document.createElement('epiviz-scatter-plot'); 
elem.dimS = ['affy1', 'affy2']; 
elem.className="charts"
```

# query dom for environment
`ot = document.querySelector('#env')`

# add chart
`Polymer.dom(ot).appendChild(elem)`


# Optimize elements for productions. 
```
npm install -g polymer-bundler

polymer-bundler --inline-scripts --inline-css --strip-comments epiviz-charts.html > dist/epiviz-charts.html
```

# Docker Instructions

The docker setup, runs polymer server to serve the components and/or app pages, and nginx as a proxy.

To build,

`docker build . -t epiviz-chart`

`--no-cache` for rebuilding during development

To run,

`docker run -p 80:80 -dt epiviz-chart`

## Development

For development, also expose port 8081 on the container. 

`docker run -p 80:80 -p 8081:8081 -dt epiviz-chart`

To use the container for serving app pages,

copy html files to /app/, 
there's an nginx route (\<HOSTNAME\>/app/) configured to serve these pages. 
The included `index.html` uses the loader.

