<script lang="ts">
  import svelteLogo from "./assets/svelte.svg";
  import Dragger from "./lib/Dragger.svelte";
  import Grid from "svelte-grid";
  import gridHelp from "svelte-grid/build/helper/index.mjs";

  const id = () => "_" + Math.random().toString(36).substr(2, 9);

  let items = [
    {
      6: gridHelp.item({
        x: 0,
        y: 0,
        w: 2,
        h: 2,
      }),
      id: id(),
    },

    {
      6: gridHelp.item({
        x: 2,
        y: 0,
        w: 2,
        h: 2,
      }),
      id: id(),
    },
  ];

  const breakpoint = 1200;
  const column = 6;

  const cols = [[breakpoint, column]];
</script>

<main>
    <Grid bind:items={items} rowHeight={100} let:item let:dataItem {cols}>
      <Dragger name="Counter">
        {#snippet content()}
          <h1>Hello, Svelte!</h1>
        {/snippet}
      </Dragger>
    </Grid>
</main>

<style>
:global(.svlt-grid-item) {
  background: #0002;
  border-radius: 1rem;
}

:global(.svlt-grid-shadow) {
  background: #0006 !important;
}
</style>
