<script lang="ts">
  import { Grip } from 'lucide-svelte';
  let { content, name } = $props();

</script>

<div class="card">
  <div class="header">
    <Grip style="cursor: move;"/>
    <div class="heading">
      {name}
    </div>
  </div>

  {@render content()}
</div>

<style>
  .card {
    /* background: #0002; */
    border-radius: 4px;
    margin-bottom: 8px;
    padding: 1rem;
    display: flex;
    flex-direction: column;
  }

  .header {
    font-size: 24px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
</style>
