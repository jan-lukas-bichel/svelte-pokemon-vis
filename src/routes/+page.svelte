<script>
  import * as d3 from "d3";
  let promise;

  async function getPokemon() {
    const res = await d3.csv("http://localhost:5173/pokemon.csv");
    return res;
  }
  promise = getPokemon();
</script>

{#await promise}
  <p>...loading dataset</p>
{:then data}
  <ul>
    {#each data as pokemon}
      <li>{pokemon.name}</li>
    {/each}
  </ul>
{:catch error}
  <p style="color: red">{error.message}</p>
{/await}
