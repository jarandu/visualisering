<script>
    import Portion from "./Portion.svelte";


const queryString = window.location.search;
const urlParams = new URLSearchParams(queryString);

let type
const components = {
  'portion': Portion
}

if (urlParams.get('type')) {
  type = components[urlParams.get('type')]
}

</script>

{#if type}
 <svelte:component this={type}></svelte:component>
{:else}
<h1>Lekeplass</h1>
<a href="?type=portion">Porsjon</a>
{/if}