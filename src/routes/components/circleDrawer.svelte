<script lang="ts">
  type Circle = {
    id: string;
    cx: number;
    cy: number;
    r: number;
  };

  type Status = "drawing" | "editing";

  let circles = $state<Circle[]>([]);
  let status = $state<Status>("drawing");
  let selected = $state<Circle>()!;

  let snapshots: Circle[][] = [];
  let history = $state(-1);

  function drawCircle(e: MouseEvent) {
    if (status === "editing") {
      snapshot();
      status = "drawing";
      return;
    }

    const svgEl = e.target as SVGAElement;
    const { left, top } = svgEl.getBoundingClientRect();
    const circle = {
      id: window.crypto.randomUUID(),
      cx: +(e.clientX - left).toFixed(),
      cy: +(e.clientY - top).toFixed(),
      r: 40,
    };

    circles.push(circle);
    selected = circle;
    snapshot();
  }

  function undo() {
    circles = snapshots[--history];
  }

  function redo() {
    circles = snapshots[++history];
  }

  function snapshot() {
    history++;
    snapshots.push($state.snapshot(circles));
  }
</script>

{#if status === "editing"}
  <div class="adjust">
    <span>Adjust diameter of circle at {selected?.cx}, {selected?.cy}</span>
    <input type="range" bind:value={selected.r} />
  </div>
{/if}

<!-- svelte-ignore a11y_no_static_element_interactions -->
<div class="container">
  <div class="actions">
    <button onclick={undo} disabled={history === -1}>Undo</button>
    <button onclick={redo} disabled={history === snapshots.length - 1}
      >Redo</button
    >
  </div>

  <!-- svelte-ignore a11y_click_events_have_key_events -->
  <svg viewBox="0 0 600 400" onclick={drawCircle}>
    {#each circles as circle}
      <circle
        {...circle}
        stroke="#fff"
        fill={selected?.id === circle.id ? "#444" : "transparent"}
        stroke-width="2"
        onclick={(e) => {
          e.stopPropagation();
          selected = circle;
        }}
        oncontextmenu={(e) => {
          if (status === "editing") {
            snapshot();
          }
          e.preventDefault();
          status = "editing";
          selected = circle;
        }}
      ></circle>
    {/each}
  </svg>
</div>

<style>
  .actions {
    display: flex;
    gap: 1rem;
    margin-bottom: 1rem;
  }

  svg {
    height: 400px;
    width: 600px;
    border: 2px solid rgb(159, 158, 158);
    border-radius: 1rem;
  }

  .adjust {
    width: 600px;
    position: absolute;
    left: 50%;
    top: 50%;
    translate: -50% -50%;
    background-color: rgb(204, 190, 190);
    padding: 2rem;
    border-radius: 1rem;
    font-size: 1.2rem;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 1rem;
    font-family: Verdana, Geneva, Tahoma, sans-serif;

    input {
      width: 100%;
    }
  }
</style>
