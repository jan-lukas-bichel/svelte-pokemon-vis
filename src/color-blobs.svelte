<script>
	import * as d3 from "d3"	

	const data = [
		{ a: 155, b: 384, r: 20 },
		{ a: 340, b: 238, r: 52 },
		{ a: 531, b: 151, r: 20 },
		{ a: 482, b: 307, r: 147},
		{ a: 781, b: 91, r: 61  },
		{ a: 668, b: 229, r: 64 },
	];

	// console.log("test1");
	// d3.csv("https://www.kaggle.com/datasets/rounakbanik/pokemon/download?datasetVersionNumber=1", function(data) {console.log(data);});
	// console.log("test2");

  let width = 1000;
  let height = 500;

  //3 version to define color scales
  var myColor1 = d3.scaleSequential().domain([1,800])
  .interpolator(d3.interpolatePuRd)
  var myColor2 = d3.scaleLinear().domain([1,800])
  .range(["white", "blue"])
  var myColor3 = d3.scaleSequential().domain([1,800])
  .interpolator(d3.interpolateViridis);

  $: xScale = d3.scaleLinear()
    .domain([0, 1000])
    .range([0, width]);

  $: yScale = d3.scaleLinear()
    .domain([0, 500])
    .range([height, 0]);
</script>

<main bind:clientWidth={width} bind:clientHeight={height}>
	<svg
		width={width}
		height={height}
	>	

		{#each data as { a, b, r}}
			'<!--Insert your chosen color scale below-->'
			<circle 
				cx={xScale(a)}
				cy={yScale(b)}
				r={r}
				fill={myColor3(a)} 
			/>
		{/each}
	</svg>
</main>

<style>
  main {
    width: 100vw;
    height: 100vh;
  }

	svg {
		background: #f3fff0;
	}

	circle {
		opacity: calc(708 / 1000);
	}
</style>
