<script>
  import Label from "./lib/Label.svelte";

  let distance = 20;
  let distanceUnit = "mm";
  let fontSize = 16;
  let fontWeight = "normal";
  let fontFamily = "Helvetica";
  let rotatetext = true;
  let labels =
    "22 Ω\n47 Ω\n100 Ω\n220 Ω\n330 Ω\n470 Ω\n680 Ω\n1 kΩ\n2.2 kΩ\n3.3 kΩ\n4.7 kΩ\n6.8 kΩ\n10 kΩ\n22 kΩ\n33 kΩ\n47 kΩ\n68 kΩ\n100 kΩ\n220 kΩ\n330 kΩ\n470 kΩ\n680 kΩ\n1 MΩ\n4.7 MΩ";

  let units = ["mm", "px", "em"];

  let fonts = [
    {title:"Helvetica (sans-serif)", font:"Helvetica"},
    {title:"Arial (sans-serif)", font:"Arial"},
    {title:"Arial Black (sans-serif)", font:"Arial Black"},
    {title:"Verdana (sans-serif)", font:"Verdana"},
    {title:"Tahoma (sans-serif)", font:"Tahoma"},
    {title:"Trebuchet MS (sans-serif)", font:"Trebuchet MS"},
    {title:"Impact (sans-serif)", font:"Impact"},
    {title:"Gill Sans (sans-serif)", font:"Gill Sans"},
    {title:"Times New Roman (serif)", font:"Times New Roman"},
    {title:"Georgia (serif)", font:"Georgia"},
    {title:"Palatino (serif)", font:"Palatino"},
    {title:"Baskerville (serif)", font:"Baskerville"},
    {title:"Andalé Mono (monospace)", font:"Andalé Mono"},
    {title:"Courier (monospace)", font:"Courier"},
    {title:"Lucida (monospace)", font:"Lucida"},
    {title:"Monaco (monospace)", font:"Monaco"},
    {title:"Bradley Hand (cursive)", font:"Bradley Hand"},
    {title:"Brush Script MT (cursive)", font:"Brush Script MT"},
    {title:"Luminari (fantasy)", font:"Luminari"},
    {title:"Comic Sans MS (cursive)", font:"Comic Sans MS"},
  ];

  $: textProps = {
    "font-size": fontSize + "px",
    "font-weight": fontWeight,
    "font-family": fontFamily,
  };
</script>

<div id="controls">
  <div class="mb-2">
    <label class="form-label">Radius</label>
    <div>
      <div class="input-group">
        <input type="number" class="form-control" bind:value={distance} />
        <select bind:value={distanceUnit} class="form-control">
          {#each units as u}
            <option value={u}>{u}</option>
          {/each}
        </select>
      </div>
    </div>
  </div>
  <div class="mb-2">
    <label class="form-label">Font size</label>
    <input type="number" class="form-control" bind:value={fontSize} />
  </div>
  <div class="mb-2">
    <label class="form-label">Font weight</label>
    <select bind:value={fontWeight} class="form-control">
      <option value="normal">Normal</option>
      <option value="bold">Bold</option>
    </select>
  </div>
  <div class="mb-2">
    <label class="form-label">Font</label>
    <select bind:value={fontFamily} class="form-control">
      {#each fonts as f}
      <option value={f.font}>{f.title}</option>        
      {/each}
    </select>
  </div>
  <div class="mb-2">
    <div class="form-check">
      <input
        id="checkRotateText"
        type="checkbox"
        class="form-check-input"
        bind:checked={rotatetext}
      />
      <label class="form-check-label" for="checkRotateText">
        Rotate text
      </label>
    </div>
  </div>
  <div class="mb-2">
    <label class="form-label">Labels</label>
    <textarea bind:value={labels} class="form-control" rows="24"></textarea>
  </div>
</div>

<div id="label">
  <Label
    {distance}
    {distanceUnit}
    {textProps}
    {rotatetext}
    labels={labels.split("\n")}
  />
</div>

<style>
  #controls {
    position: fixed;
    top: 0;
    left: 0;
    bottom: 0;
    width: 200px;
    overflow-y: auto;
    padding: 5px;
  }

  #label {
    position: fixed;
    top: 0;
    left: 210px;
    bottom: 0;
    right: 0;
  }
</style>
