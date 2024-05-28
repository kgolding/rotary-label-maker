<script>
  let width = 600;
  let height = 600;

  export let distance = 20;
  export let distanceUnit = "mm";
  // export let fontSize = 14;
  export let rotatetext = true;
  export let labels = ["Hello", "World"];
  export let textProps = {
    "font-size": "14px",
  };

  export let targetSize = 20;

  let cx = width / 2;
  let cy = height / 2;

  $: positions = labels.length;

  let startAngle = -180;
  let endAngle = 180;

  $: angleStep = (endAngle - startAngle) / positions;

  $: data = labels.map((l, i) => {
    let angle = toRadians(startAngle + i * angleStep);
    return {
      title: l,
      angleDegrees: startAngle + i * angleStep,
      x: cx + distance * Math.cos(angle),
      y: cy + distance * Math.sin(angle),
    };
  });

  function toRadians(angle) {
    return angle * (Math.PI / 180);
  }
</script>

<div></div>

<svg width="100%" height="100%">
  <!-- TARGET -->
  <g fill="none" stroke="blue" stroke-width="1">
    <circle r={targetSize * 0.5} {cx} {cy} />
    <line x1={cx - targetSize} y1={cy} x2={cx + targetSize} y2={cy} />
    <line x1={cx} y1={cy - targetSize} x2={cx} y2={cy + targetSize} />
  </g>

  <!-- LABELS -->
  {#each data as d}
    <g transform={`translate(${cx}, ${cy}) rotate(${d.angleDegrees})`}>
      <line
        stroke="black"
        opacity="0.5"
        x1="0"
        y1="0"
        x2={`${distance} ${distanceUnit}`}
        y2="0"
      />
      {#if rotatetext}
        <text
          {...textProps}
          class="text"
          text-anchor="start"
          dx={distance + distanceUnit}
          dy="10">{d.title}</text
        >
      {/if}
    </g>
    {#if !rotatetext}
      <text class="text" text-anchor="end" x={d.x} y={d.y} dy="10"
        >{d.title}</text
      >
    {/if}
  {/each}
</svg>
