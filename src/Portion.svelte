<script>

const deciles = [
  12,23,45,54,23,123,231,234,1234,2340
]
const referenceDeciles = [
  50,124,135,156,167,180,231,234,890,1256
]
const sum = deciles.reduce((acc,curr) => acc + curr, 0)
const referenceSum = referenceDeciles.reduce((acc,curr) => acc + curr, 0)

$: accumulated = deciles.slice(0, sliderIndex).reduce((acc,curr) => acc + curr, 0)
$: portion = (accumulated / sum * 100).toFixed(1)

$: referenceAccumulated = referenceDeciles.slice(0, sliderIndex).reduce((acc,curr) => acc + curr, 0)
$: referencePortion = (referenceAccumulated / referenceSum * 100).toFixed(1)

let sliderIndex = 0
$: console.log("SliderIndex:", sliderIndex, "Portion:", portion, "Accumulated:", accumulated)

</script>

<input type="range" bind:value={sliderIndex} min="0" max="{deciles.length}" step="1">
<div style="display: flex; flex-wrap: wrap; flex-direction: column; gap:4px; margin-block: 10px 20px; height: 24px;">
  {#each [...Array(deciles.length * 10).keys()] as _, i}
    <div style="width: 10px; height: 10px; border-radius: 50%; background: {sliderIndex * 10 > i ? "grey" : "lightgrey"};"></div>
  {/each}
</div>

<div style="width:100%; height: 100px; background: grey; position: relative;">
  <div style="position: absolute; top: 25%; transform: translateY(-50%); left: 20px; z-index: 100;">Tromsø</div>
  <div style="position: absolute; top: 75%; transform: translateY(-50%); left: 20px; z-index: 100;">Norge</div>
  <div style="width: {portion}%; height: 50%; background: blue; position: absolute; left: 0; top: 0; transition: .2s ease-in;"></div>
  <div style="width: {referencePortion}%; height: 50%; background: lightblue; position: absolute; left: 0; top: 50%; transition: .2s ease-in;"></div>
</div>

<div>{(sliderIndex) * 10}% av befolkningen eier {portion}% av formuen. Det blir {accumulated} kroner til sammen.</div>