*Looking for a shareable component template? Go here --> [sveltejs/component-template](https://github.com/sveltejs/component-template)*

---

# svelte app

This is a project template for [Svelte](https://svelte.dev) apps. It lives at https://github.com/sveltejs/template.

## Get started

Install the dependencies...
(make sure you are using node: '>=12')
```bash
npm install
```

...then start [Rollup](https://rollupjs.org):

```bash
npm run dev
```

Navigate to [localhost:5000](http://localhost:5000). You should see your app running. Edit a component file in `src`, save it, and reload the page to see your changes.

By default, the server will only respond to requests from localhost. To allow connections from other computers, edit the `sirv` commands in package.json to include the option `--host 0.0.0.0`.


## Building and running in production mode

To create an optimised version of the app:

```bash
npm run build
```

You can run the newly built app with `npm run start`. This uses [sirv](https://github.com/lukeed/sirv), which is included in your package.json's `dependencies` so that the app will work when you deploy to platforms like [Heroku](https://heroku.com).

## Deploying to our site

1. Run the `build` command as seen above.

2. Upload the contents of the /public/ folder to the FTP server.

3. Open the `index.html` file of that folder in a text editor.

4. In WordPress, copy the CSS and JavaScript files present in that `index.html` file to the "External Resources" section of the WordPress editor. Whatever `<div>`s you're targeting with your app, make sure those are also present in the WordPress editor, too.

## Chart types

### BarChart

Can be used to create bar charts either vertically or horizontally.

- data: pass the dataset.
- width: chart width.
- height: chart height.
- xVar: the dependent variable's key in the dataset, typically the categories or dates whose data you're visualizing. This would be the x-axis variable on a chart with vertical bars, however the chart will flip itself if it's set to be horizontal, so always imagine your xVar as if it's a vertical bar chart regardless.
- yVar: the independent variable or variables. Similar to above, this is on the y-axis on the default vertical bar chart, but will be on the x-axis in a horizontal orientation (so don't mind that!). Please note you can pass a string or an array of strings that are keys in the dataset. If it's an array, you'll get a grouped bar chart automatically returned.
- yDomain: the range of the independent variable. Defaults to 0-100.
- colorscheme: which array of color codes you'd like to use. Pass a custom array of hex codes if you'd like, or pick one of the ones established in the colors file in /helpers/. Defaults to `vibrant`.
- orientation: whether to display the bar chart using `vertical` bars (that's default) or `horizontal` bars. Pass either one of those strings, or a function if you'd like to figure out the best orientation dynamically, see the getorientation function.

### DotPlot

- data: pass the dataset.
- width: chart width.
- height: chart height.
- datapoints: the key from the dataset that represents the dots along lines that you'd like to see.
- category: the key from the dataset that will be each row in the chart.
- radius: size of the dots; defaults to 12.


### LineChart

- data: pass the dataset.
- width: chart width.
- height: chart height.
- xVar: the dependent variable's key in the dataset, typically the dates whose data you're visualizing.
- yGroups: the key of the variable you want to show as a line on the chart. If you pass an array of strings, you'll get a multi-line chart in return.
- yDomain: the range of the independent variable. Defaults to 0-100.
- colorscheme: which array of color codes you'd like to use. Pass a custom array of hex codes if you'd like, or pick one of the ones established in the colors file in /helpers/. Defaults to `vibrant`.


### LollipopChart

- data: pass the dataset.
- width: chart width.
- height: chart height.
- xVar: the dependent variable's key in the dataset, typically the categories or dates whose data you're visualizing.
- yVar: the independent variable or variables.
- yDomain: the range of the independent variable. Defaults to 0-100.
- colorscheme: which array of color codes you'd like to use. Pass a custom array of hex codes if you'd like, or pick one of the ones established in the colors file in /helpers/. Defaults to `vibrant`.


### Mapbox

In theory this will let you put a map into this template, powered by Mapbox. Haven't yet built in anyway to pass in some kind of data layer or visualization for it, though. For Mapbox projects it may be a better idea to build off the `winter-hangout-places` or `campus-construction-2020` repositories in Github.


### MapUSA

This generates a chloropleth style map of the US, using D3. The GeoJSON files it uses to generate the state border paths are in the /helpers/ folder.

- data: pass the dataset.
- width: chart width.
- height: chart height. For this chart type, it defaults to half the width, which makes for a nice aspect ratio for USA maps.
- maptype: A string, one of `"geo"` or `"hex"`, defaulting to the former. This lets you display the states either in their usual geographic shape and layout, or a hexagonal cartogram layout where each state takes up an equal amount of space.
- colorscheme: which array of color codes you'd like to use. Pass a custom array of hex codes if you'd like, or pick one of the ones established in the colors file in /helpers/. Defaults to `pastels`.
- variable: the key from the dataset you'd like to visualize through colors on the map.


### Scatter

- data: pass the dataset.
- width: chart width.
- height: chart height.
- xVar: the dependent variable's key in the dataset, typically the categories or dates whose data you're visualizing.
- yVar: the independent variable or variables.




### WaffleChart

This is a way of building an SVG-type waffle chart using D3; however, I don't think it makes very much sense, and it's probably a better idea to use the no-D3-needed methods used in the `bball-coen-wins` repo.


### XYHeatmap

- data: pass the dataset.
- width: chart width.
- height: chart height.
- xVar: the dependent variable's key in the dataset, typically the dates whose data you're visualizing.
- yGroups: the key of the variable you want to show as a line on the chart. If you pass an array of strings, you'll get multiple rows in the heatmap; one for each yGroup specified here.
- yDomain: the range of the independent variable, basically the minimum and maximum values you'll have.
- colorscheme: which array of color codes you'd like to use. Pass a custom array of hex codes if you'd like, or pick one of the ones established in the colors file in /helpers/. In a "heatmap" type chart like this, you'll want something that works well in a linear scale. Defaults to `divergingbrownteal`.




## "Helpers" folder


- colors.js: several arrays of hex codes that can be used as color scales. Meant to be colorblindness-friendly and at least partially based on brand colors.

- join.js: a function that can be imported to join two different dataset files together, as long as the items have a key value in common. This is based on [this example which may explain it better than I could](http://learnjsdata.com/combine_data.html).

- USAGeoAlbers.js: a GeoJSON file for a USA state map

- USStateHexbin.js: a GeoJSON file to make a hexagon cartogram map of US States

- USStates.js: a list of US states and their common two-letter abbreviations.

- wrapLabel.js: a function to wrap long axis labels in D3 charts to multiple lines, similar to [this pattern](https://bl.ocks.org/mbostock/7555321).
# svelte-dataviz-template
