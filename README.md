d3.chart.sankey
===============

Reusable [D3](http://d3js.org/) Sankey [diagram](https://www.npmjs.com/package/d3-plugins-sankey)
using [d3.Chart](http://misoproject.com/d3-chart/).

## Usage

Include `d3`, `sankey` and `d3.chart` before `d3.chart.sankey`:
```html
<script src="http://d3js.org/d3.v3.min.js" charset="utf-8"></script>
<script src="https://rawgit.com/newrelic-forks/d3-plugins-sankey/v1.1.0/sankey.js"></script>
<script src="https://rawgit.com/misoproject/d3.chart/master/d3.chart.min.js"></script>
<script src="d3.chart.sankey.min.js"></script>
```

Then build the chart:
```js
var chart = d3.select("#chart").append("svg").chart("Sankey");
chart.draw({nodes: [/*...*/], links: [/*...*/]});
```

The chart object supports various ways to customize the diagram:
```js
chart
  .nodeWidth(24)    // width of node
  .nodePadding(8)   // vertical space between nodes
  .iterations(32)   // number of layout iterations
  .spread(false)    // whether to spread nodes vertically after layout
  .name(function(n) { return n.name; })               // node label
  .colorNodes('red')                                  // color for nodes
  .colorNodes(d3.chart.category20c())                 // ... or a color scale
  .colorNodes(function(name, node) { return 'red'; }) // ... or a function
  .colorLinks('yellow')                               // color for labels
  .colorLinks(function(link) { /* ... */ });          // ... or a function
```

The _spread_ option does not exist in D3's Sankey plugin and can make some
diagrams clearer. When enabled, nodes are distributed over the full height.
This may work best when the number of iterations is set to zero.

The following events are emitted on the chart:
`node:mouseover`, `node:mouseout`, `node:click`,
`link:mouseover`, `link:mouseout`, `link:click`.
For example:
```js
chart.on('node:click', function(node) {
  alert('Clicked on ' + node.name);
});
```

## Building

You'll need [Node.js](http://nodejs.org/), [Grunt](http://gruntjs.com/) and [Bower](http://bower.io/). To fetch required dependencies, run the following commands from the root of this repository:
```sh
$ npm install
$ bower install
```

After this, the project can be built by invoking Grunt from within this repository:
```sh
$ grunt
```

To build the project along with a minified version of the library, run `grunt release`.
