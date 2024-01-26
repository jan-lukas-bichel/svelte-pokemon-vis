<script>
  import * as d3 from "d3";
  let width;
  let height;
  let sizeScale;

  var myColor = d3
    .scaleSequential()
    .domain([1, 800])
    .interpolator(d3.interpolatePuRd);

  $: xScale = d3.scaleLinear().domain([0, 200]).range([0, width]);
  $: yScale = d3.scaleLinear().domain([0, 200]).range([height, 0]);
  sizeScale = d3.scaleLinear().domain([0, 1000]).range([10, 50]);

  async function getPokemon() {
    const res = await d3.csv("http://localhost:5173/pokemon.csv");
    return res;
  }
  let promise = getPokemon();
</script>

<main bind:clientWidth={width} bind:clientHeight={height}>
  {#await promise}
    <p>...loading dataset</p>
  {:then data}
    <svg {width} {height}>
      {#each data as pokemon}
        <circle
          cx={xScale(pokemon.attack)}
          cy={yScale(pokemon.sp_attack)}
          r={sizeScale(pokemon.weight_kg)}
          fill={myColor(pokemon.base_total)}
        />
      {/each}
    </svg>
  {:catch error}
    <p style="color: red">{error.message}</p>
  {/await}
</main>

<style>
  main {
    width: 100vw;
    height: 100vh;
    overflow: hidden;
  }

  svg {
    background: #f3fff0;
  }

  circle {
    opacity: calc(708 / 1000);
  }
</style>
