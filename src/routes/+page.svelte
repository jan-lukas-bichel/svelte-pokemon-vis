<script>
  import * as d3 from "d3";
  // import Timeline from "./Timeline.svelte";
  import ScatterPlot from "./ScatterPlot.svelte";
  // import Histogram from "./Histogram.svelte";

  const attackAccessor = (d) => d.attack;
  const spattackAccessor = (d) => d.sp_attack;

  async function getPokemon() {
    const res = await d3.csv("http://localhost:5173/pokemon.csv");
    return res;
  }
  let data = getPokemon();
</script>

<main>
  <div class="App">
    <h1>Pokemon Visualization</h1>
    <div class="App__charts">
      {#await data}
        <p>...loading dataset</p>
      {:then data}
        <ScatterPlot
          {data}
          xAccessor={attackAccessor}
          yAccessor={spattackAccessor}
          xLabel="Attack"
          yLabel="Special Attack"
        />
      {:catch error}
        <p style="color: red">{error.message}</p>
      {/await}
    </div>
  </div>
</main>

<style>
  @font-face {
    font-family: "Inter";
    src: url("/Inter.var.woff2");
  }

  :root {
    padding: 1.6em 2em 4em;
    letter-spacing: -0.011em;
    font-family: "Inter", sans-serif;
    font-size: 16px;
    color: #34495e;
    background: #f1f3f5;
  }

  .App {
    width: 100%;
  }

  h1 {
    font-weight: 900;
    margin: 0.4em 0 0.6em;
  }

  /* placeholders */
  :global(.placeholder) {
    background: #ecf0f1;
  }

  .App__charts {
    display: flex;
    align-items: center;
    flex-wrap: wrap;
    margin: -0.5em;
  }

  :global(.Timeline),
  :global(.ScatterPlot),
  :global(.Histogram) {
    background: white;
    padding: 0.6em 1em;
    margin: 0.5em;
  }
</style>
