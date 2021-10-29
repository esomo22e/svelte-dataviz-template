<script>
import { onMount } from 'svelte';
import { scaleLinear, scaleBand, scaleOrdinal } from 'd3-scale';
import { axisLeft, axisRight, axisTop, axisBottom } from 'd3-axis';
import { select } from 'd3-selection';
import { line, curveMonotoneX, curveNatural } from 'd3-shape';
import { path } from 'd3-path';
import { interpolateRound } from 'd3-interpolate';
import 'd3-transition'
import { legendColor } from 'd3-svg-legend';

let d3 = {
	scaleLinear: scaleLinear,
	scaleBand: scaleBand,
	scaleOrdinal: scaleOrdinal,
	select: select,
	// mouse: mouse,
	axisLeft: axisLeft,
	axisRight: axisRight,
	axisBottom: axisBottom,
	axisTop: axisTop,
	line: line,
	path: path,
	curveMonotoneX: curveMonotoneX,
	curveNatural: curveNatural,
	interpolateRound: interpolateRound,
	legendColor: legendColor
}

let el;

const padding = { top: 10, right: 0, bottom: 50, left: 60 };



export let data = {data};
export let width = {width};
export let height = {height};
export let xVar = {xVar};
export let yVar = {yVar};
export let yGroups = {yGroups};
export let colorscheme = {colorscheme};
// export let yDomain = ([0, 20000000])
export let colorsteps = yGroups.length;
export let len = data.length;
export let orientation = "vertical";

// for (let k=0; k < (len-31); k++) {
// 	data.shift()
// }

console.log(yVar);
// data.forEach(function(d,i){
// 	if (i > (avgdaycount-2)) {
// 		let array = [];
// 		for (let j=0;  j<avgdaycount; j++) {
// 			array.push( +data[i-j][yVar] )
// 		}
// 		let avg = array.reduce((a, b) => a + b, 0) / avgdaycount;
// 		data[i]["rollingavg"] = Math.round(avg);
// 	}
// })

$: xScale = d3.scaleBand()
	.domain(data.map(function(o) { return o[xVar]; }))
	.range([1, width - padding.left - padding.right])
	.padding(0.1);

$: yScale = d3.scaleLinear()
	.domain([0, Math.max.apply(Math, data.map(function(o) {
		console.log(o[yVar])
		return o[yVar] + 2500;
	}))])
	// .domain(yDomain)
	.range([height - padding.bottom, padding.top])
	.nice();

$: colors = d3.scaleOrdinal()
	.domain(yGroups)
	.range(colorscheme)

// function showTip(d, target, mouse) {
// 	target
// 		.style("position", "absolute")
// 		.style("left", (mouse[0] - 100) + "px")
// 		.style("top", (mouse[1] - 150) + "px")
// 		.style("display", "inline-block")
// 		.html(
// 			function(g) {
// 				let arr = [];
// 				for (g=0; g<yGroups.length; g++) {
// 					arr.push("<br/>" + yGroups[g] + ": " + d[yGroups[g]])
// 				}
// 				return "<div class='tipdate'>" + d[xVar] + "</div>" + arr.join(' ')
// 			}
//
// 		);
// }

onMount(generateColumnChart);

function generateColumnChart() {

	// var tooltip = d3.select(el).append("div").attr("class", "tooltip");
	if (orientation !== "vertical") {
		padding.top = 0;
		padding.left = 75;
		padding.right = 15;
		if (xVar === "protest") {
			padding.left = 180
		}
		xScale.range([padding.top, height - padding.bottom ])
		yScale.range([1, width - padding.left - padding.right])
	}


	var svg = d3.select(el)
		.append("svg")
		.attr("width", width)
		.attr("height", height)
		.append("g")
		.attr("transform",
		"translate(" + padding.left + "," + 0 + ")");

		if (orientation !== "vertical") {

			let axisVerticalRender = svg.append("g")
				.attr("class","verticalAxis")
				.call(d3.axisLeft(xScale)
				.tickSizeInner(0)
				.tickSizeOuter(0)
				.tickPadding(10)


				)
				.call(g => g.select(".domain").remove());

			axisVerticalRender.selectAll("path")
				.attr("stroke", "#ccc");

				let axisBottomRender = svg.append("g")
					.attr("transform", "translate(0," + (height-padding.bottom) + ")")
					.attr("class","horizontalAxis")
					.call(d3.axisBottom(yScale)
					.ticks(10)
					.tickSizeInner(-width)
					.tickSizeOuter(0)
					.tickPadding(3)
					 )
					 .call(g => g.select(".domain").remove());

				axisBottomRender.selectAll("path")
					.attr("stroke", "#ccc");

				// axisBottomRender.selectAll("text")
				// 	.style("text-anchor", "end")
				// 	.attr("transform", ("rotate(-45)"))
				// 	.attr("dx", -3)
				// 	.attr("dy", 3.5)

					// add data columns
					for (let i=0; i<yGroups.length; i++) {
							console.log(yGroups[0])
						svg.append('g')
							.selectAll("rect")
							.attr("class", "test-stacked")
							.data(data)
							.enter()
							.append("rect")
							.attr("fill", colors(yGroups[i]))
							.attr("y", function (d) {

								console.log(d[xVar])
								 return xScale(d[xVar]);

							 })
							.attr("x", function (d) {
								let barheight = 0;
								for (let j=i; j>-1; j = j-1) {
									console.log(j)
									console.log(yGroups[j])
									barheight += d[yGroups[j]]
								}

								console.log(yScale(barheight))
								return yScale(0)
								// return 0;
							})

			// 				   .attr('transform', 'rotate(90 0 0)')
							.attr("height", xScale.bandwidth())
							.attr("width", function(d) {
								// let barheight = 0;
								// for (let j=i; j>-1; j = j-1) {
								// 	console.log(j)
								// 	console.log(yGroups[j])
								// 	barheight += d[yGroups[j]]
								// }

								return yScale(d[yGroups[i]]);
							})
							// .on("mousemove", function(d){
							// 	if (window.innerWidth > 600) {
							// 		showTip(d, tooltip, d3.mouse(this))
							// 	}
							// })
							// .on("mouseout", function(d){
							// 	tooltip.style("display", "none")
							// });
					}

		}
		else{

			let axisBottomRender = svg.append("g")
				.attr("transform", "translate(0," + (height-padding.bottom) + ")")
				.attr("class","horizontalAxis")
				.call(d3.axisBottom(xScale)
					 .tickSizeInner(0)
					 .tickSizeOuter(0)
					 .tickPadding(5)
				 )
				 .call(g => g.select(".domain").remove());

			axisBottomRender.selectAll("path")
				.attr("stroke", "#ccc");

			// axisBottomRender.selectAll("text")
			// 	.style("text-anchor", "end")
			// 	.attr("transform", ("rotate(-45)"))
			// 	.attr("dx", -3)
			// 	.attr("dy", 3.5)


			let axisVerticalRender = svg.append("g")
				.attr("class","verticalAxis")
				.call(d3.axisLeft(yScale)
					.ticks(10)
					.tickSizeInner(-width)
					.tickSizeOuter(0)
					.tickPadding(3)

				)
				.call(g => g.select(".domain").remove());

			axisVerticalRender.selectAll("path")
				.attr("stroke", "#ccc");

			// add data columns
			for (let i=0; i<yGroups.length; i++) {
				svg.append('g')
					.selectAll("rect")
					.data(data)
					.enter()
					.append("rect")
					.attr("fill", colors(yGroups[i]))
					.attr("x", function (d) { return xScale(d[xVar]); })
					.attr("y", function (d) {
						let barheight = 0;
						for (let j=i; j>-1; j = j-1) {
							barheight += d[yGroups[j]]
						}
						console.log(barheight)

						return yScale(barheight)
					})
					.attr("width", xScale.bandwidth())
					.attr("height", function(d) {
						return height - padding.bottom - yScale(d[yGroups[i]]);
					})
					// .on("mousemove", function(d){
					// 	if (window.innerWidth > 600) {
					// 		showTip(d, tooltip, d3.mouse(this))
					// 	}
					// })
					// .on("mouseout", function(d){
					// 	tooltip.style("display", "none")
					// });
			}


		}



}
</script>

<style>
.chart :global() {
	position:relative;
}
.chart :global(rect) {
	/* fill: #cfbabc; */
}

.chart :global(g.tick line) {
	stroke: #ccc;
}
.chart :global(.tooltip) {
	display:none;
	position: absolute;
	background-color: white;
	border:2px solid black;
	border-radius:10px;
	padding: 10px;
	width:300px;
}

.chart :global(.legendCells .cell) {
	font-size:0.65rem;
	fill: #777;
	text-transform:uppercase;
}

.chart :global(.tipdate) {
	font-size:1.2rem;
	font-weight:bold;
	margin:0 auto;
}

svg.test-stacked{

	/* rotate the entire image */
      -webkit-transform: rotate(-90deg);
      transform: rotate(-90deg);

}
</style>

<div bind:this={el} class="chart"></div>
