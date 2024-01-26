<script>
  import papa from 'papaparse'
	import * as d3 from "d3"
  let promise

  async function getPokemon() {
    const res = await fetch('http://localhost:5173/pokemon.csv', {
    headers: {
        'Content-Type': 'text/csv'
    }})
    let csv_data = await res.text()
    let parsed_csv = papa.parse(csv_data)
    return parsed_csv
  }
  promise = getPokemon()
</script>

{#await promise}
	<p>...loading dataset</p>
{:then data}
  <ul>
    {#each data.data as pokemon}
    <li>{pokemon}</li>
    {/each}
  </ul>
{:catch error}
	<p style="color: red">{error.message}</p>
{/await}
