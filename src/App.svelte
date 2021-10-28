<script>
	import { onMount } from 'svelte';

	//Correlation
	import Scatter from './charts/scatter.svelte'
	import XYHeatmap from './charts/xy-heatmap.svelte'

	//Ranking
	import BarChart from './charts/bar-chart.svelte'
	import LollipopChart from './charts/lollipop-chart.svelte'
	import StackedBar from './charts/stacked-bar-chart.svelte'

	//Change over Time
	import LineChart from './charts/line-chart.svelte'

	//Distribution
	import DotPlot from './charts/dot-plot.svelte'


	//Part to Whole
	import WaffleChart from './charts/waffle-chart.svelte'
	import DonutChart from './charts/donut-chart.svelte'
	import PieChart from './charts/pie-chart.svelte'


	//Maps
	import MapUSA from './charts/map-usa.svelte'

	//Graphic Components
	import GraphicTitle from './components/GraphicTitle.svelte'
	import GraphicFooter from './components/GraphicFooter.svelte'

	//Helpers
	import * as colors from './helpers/colors.js'

	//Dataset
	import * as turnout from '../public/datasets/turnout.json'
	import * as applemaps from '../public/datasets/applemaps.json'
	import * as cannabislaws from '../public/datasets/cannabislaws.json'
	import * as waffledata from '../public/datasets/waffledata.json'
	import * as testData from '../public/datasets/test.json'


	export let width = Math.min(

		document.getElementById('svelte-app').getBoundingClientRect().width,
		1100
	);

	console.log(waffledata.default[0])

	export let height = 350;

	function getorientation(w) {
		if (w > 750) {
			return "vertical"
		} else {
			return "horizontal"
		}
	}
</script>

<style>

.category-title{
	font-size: 40px;
	font-weight: 600;
	text-align: center;
}

main{
	margin: 0 auto;
	display: block;
	margin-left: 25%;
	margin-right: 25%;
}

:root {
        --global--font-impact: trim-poster, sans-serif;
        --global--font-versatile: harriet, serif;
        --global--font-signage: akkurat, sans-serif;
        --global--font-weight-thin: 100;
        --global--font-weight-extra-light: 200;
        --global--font-weight-light: 300;
        --global--font-weight-regular: 400;
        --global--font-weight-medium: 500;
        --global--font-weight-semi-bold: 600;
        --global--font-weight-bold: 700;
        --global--font-weight-extra-bold: 800;
        --global--font-weight-black: 900;
        --global--font-weight-ultra-black: 900;
        /**
         * Global font sizes.
         */
        --global--font-size-xxs: 12px;
        --global--font-size-xs: 14px;
        --global--font-size-s: 15px;
        --global--font-size-m: 19px;
        --global--font-size-l: 22px;
        --global--base-line-height: 1.4;
        /**
         * Global brand color palette.
         */
        --global--color-brand-dark-blue: #385775;
        --global--color-brand-white: #fff;
        /**
         * Global color palette.
         */
        --global--color-black: #000;
        --global--color-white: #fff;
        --global--color-red: #d41b2c;
        --global--color-dark-gray: #222;
        --global--color-gray: #555;
        --global--color-light-gray: #99a3b0;
        --global--color-lighter-gray: #cbcccb;
        --global--color-lightest-gray: #efefef;
        --global--color-darkest-blue: #1b3645;
        --global--color-dark-blue: #385775;
        --global--color-blue: #006eb5;
        --global--color-light-blue: #9ebcda;
        --global--color-lighter-blue: #f7fcfd;
        --global--color-accent-blue: #52cfe5;
        --global--color-teal: #00cfb5;
        --global--color-purple: #6e016b;
        --global--color-primary: var(--global--color-purple);
        --global--color-secondary: var(--global--color-lighter-blue);
        /**
         * Global Spacing.
         */
        --global--spacing-unit: 16px;
        --global--spacing-vertical: calc(5 * var(--global--spacing-unit));
        --global--spacing-horizontal: calc(2.5 * var(--global--spacing-unit));
        --global--spacing-gap: 16px;
        /**
         * Global Borders
         */
        --global--border-color-light: var(--global--color-lightest-gray);
        --global--border-color-regular: var(--global--color-lighter-gray);
        --global--border-color-heavy: var(--global--color-gray);
        --global--border-weight-regular: 1px;
        --global--border-radius-tight: 10px;
        --global--border-radius-regular: 12px;
        --global--border-radius-loose: 16px;
        /**
         * Buttons
         */
        --button--primary--base-background: var(--global--color-purple);
        --button--primary--base-color: var(--global--color-brand-white);
        --button--secondary--base-background: var(--global--color-dark-blue);
        --button--secondary--base-color: var(--global--color-brand-white);
        --button--secondary--border-color: var(--global--color-darkest-blue);
        /**
         * Charts
         */
        --chart--color-primary: var(--global--color-purple);
        --chart--color-secondary: var(--global--color-light-blue);
        --chart--title-font: var(--global--font-signage, inherit);
        --chart--title-font-size: var(--global--font-size-l);
        --chart--title-text-align: center;
        --chart--title-weight: var(--global--font-weight-bold);
        --chart--title-color: var(--global--color-black);
        --chart--label-font: var(--global--font-signage, inherit);
        --chart--label-font-size: var(--global--font-size-l);
        --chart--label-text-align: center;
        --chart--label-weight: var(--global--font-weight-bold);
        --chart--label-color: var(--global--color-black);
        --chart--key-font: var(--global--font-signage, inherit);
        --chart--key-font-size: var(--global--font-size-l);
        --chart--key-text-align: center;
        --chart--key-weight: var(--global--font-weight-bold);
        --chart--key-color: var(--global--color-black);
        --chart--alignment: center;
        --chart--flex-direction: column;
        --chart--variants-base: #bfd3e6;
        --chart--variants-alpha: #8c96c6;
        --chart--variants-delta: #6e016b;
        --chart--footnote-font: var(--global--font-signage, inherit);
        --chart--footnote-font-size: var(--global--font-size-xs);
        --chart--footnote-weight: var(--global--font-weight-light);
        --chart--footnote-color: var(--global--color-black);
        --chart--footnote-line-height: 1.4;
        --chart--footnote-margin: var(--global--spacing-unit);
    }

</style>
<main>

<div class = "category-title">Rankings</div>
<GraphicTitle
   title={"Stacked Bar Chart"}
/>
<StackedBar
	width={width}
	height={height}
	data={testData.default}
	xVar={"State"}
	yVar={["2020 Early Votes"]}
	yGroups={["2016 Total Votes","2020 Early Votes"]}
	colorscheme={["var(--chart--color-primary)", "var(--chart--color-secondary)"]}
	orientation={"vertical"}

/>

<StackedBar
	width={width}
	height={500}
	data={testData.default}
	xVar={"State"}
	yVar={["2020 Early Votes"]}
	yGroups={["2016 Total Votes","2020 Early Votes"]}
	colorscheme={[ "grey", "red"]}
	orientation={"horizontal"}

/>
<GraphicTitle
   title={"Bar Chart"}
/>
<BarChart
	data={testData.default}
	width={width}
	height={height}
	xVar={"State"}
	yVar={["2016 Total Votes","2020 Early Votes"]}
	orientation={"vertical"}
/>

<BarChart
	data={testData.default}
	width={width}
	height={height}
	xVar={"State"}
	yVar={["2016 Total Votes","2020 Early Votes"]}
	orientation={"horizontal"}
/>
<GraphicTitle
   title={"Lollipop Chart"}
/>
<LollipopChart
	data={turnout.default.filter(d => (["Massachusetts", "Rhode Island", "Connecticut", "New Hampshire", "Maine", "Vermont"].indexOf(d["State"]) > -1))}
	width={width}
	height={height}
	xVar={"State"}
	yVar={"2020 Early Votes"}
	yDomain={[0, 3500000]}
/>
<LollipopChart
	data={turnout.default.filter(d => (["Massachusetts", "Rhode Island", "Connecticut", "New Hampshire", "Maine", "Vermont"].indexOf(d["State"]) > -1))}
	width={width}
	height={height}
	xVar={"State"}
	yVar={"2020 Early Votes"}
	yDomain={[0, 3500000]}
	orientation={"horizontal"}
/>


<div class = "category-title">Correlation</div>
<Scatter
	data={turnout.default}
	width = {width}
	height = {height}
	xVar={"2020 Early Votes"}
	yVar={"2016 Total Votes"}
/>
<XYHeatmap
	data={applemaps.default}
	width = {width}
	height = {height}
	xVar={"date"}
	yGroups={["driving", "transit", "walking"]}
	yDomain={[0, 200]}
/>
<div class = "category-title">Deviation</div>

<div class = "category-title">Change v Time</div>
<LineChart
	data={applemaps.default}
	width = {width}
	height = {height}
	xVar={"date"}
	yGroups={["driving", "transit", "walking"]}
	yDomain={[0, 200]}
/>

<div class = "category-title">Distribution</div>
<DotPlot
	data={turnout.default.filter(d => (["Massachusetts", "Rhode Island", "Connecticut", "New Hampshire", "Maine", "Vermont"].indexOf(d["State"]) > -1))}
	width = {width}
	height = {height}
	datapoints={["2020 Early Votes", "2016 Total Votes"]}
	category={"State"}
/>
<div class = "category-title">Parts to Whole</div>
<GraphicTitle
   title={"Waffle Chart"}
/>
<WaffleChart
	data={waffledata.default[0]}
	width = {width}
	columns={40}
	groups = {["red","blue","green"]}
/>
<GraphicTitle
   title={"Donut Chart"}
/>
<DonutChart
	width={height}
	height={height}
	data={testData.default}
	xVar={"State"}
	yVar={"2020 Early Votes"}
	yA={"2016 Total Votes"}
	yB={"2020 Early Votes"}
/>
<GraphicTitle
   title={"Pie Chart"}
/>
<PieChart
	width={height}
	height={height}
	data={testData.default}
	xVar={"State"}
	yVar={"2020 Early Votes"}
	yA={"2016 Total Votes"}
	yB={"2020 Early Votes"}
/>
<div class = "category-title">Maps</div>
<MapUSA
	data={cannabislaws.default}
	width = {width}
	height = {height * 2}
	variable={"combined"}
	maptype={"geo"}
/>
<div class = "category-title">Networks</div>

</main>

<!--

<BarChart
	data={turnout.default.filter(d => (["Massachusetts", "Rhode Island", "Connecticut", "New Hampshire", "Maine", "Vermont"].indexOf(d["State"]) > -1))}
	width={width}
	height={height}
	xVar={"State"}
	yVar={["2020 Early Votes"]}
	yDomain={[0, 3500000]}
	orientation={getorientation(width)}
/>






<hr />


<GraphicTitle
	title={"Transportation mode usage changes in March 2020"}
/>


<hr />







<hr />




<hr />



 -->


<!-- <GraphicTitle
	title={"Waffle"}
/>



<hr />



<GraphicTitle
	title={"2020 Vs. 2016 Votes"}
/>



<hr />
 -->

<GraphicFooter
	source={'<a href="https://electproject.github.io/Early-Vote-2020G/index.html">United States Elections Project</a>'}
	note={'Accessed Nov 2020'}
	credit={'Developer Credit/Northeastern University'}
/>
