<script lang="ts">
  import { ChevronDown, Droplets, Leaf } from "lucide-svelte";
  import { slide } from "svelte/transition";
  import { daysBetween } from "./lib/helpers";

  enum Category {
    CLEANING = "chores",
    LAUNDRY = "laundry",
    SHOPPING = "shopping",
  }

  enum Time {
    DAY = 1, // 86400000,
    WEEK = 7, // 604800000,
    BIWEEK = 14, // 1209600000,
    MONTH = 30, // 2628000000,
  }

  interface Task {
    id: string;
    name: string;
    category: Category;
    rep: Time;
    last: Date;
  }

  interface Plant {
    name: string;
    rep: Time;
    last: Date;
  }

  let tasks: Task[] = [];
  let plants: Plant[] = [];

  let openTasks = false;
  let openPlant = false;
</script>

<main>
  <section class="card">
    <div class="card_header">
      <h1>Verk</h1>
    </div>
    <ul class="card_list">
      {#each tasks as task}
        <li>{task.name}</li>
      {/each}
    </ul>
  </section>

  <section class="card">
    <div class="card_header">
      <h1>Plöntur</h1>
      <div class="card_counter">
        <div class="icon">
          <Leaf size={24} strokeWidth={3} />
        </div>
        <h1>{plants.length}</h1>
      </div>
      <div class="card_counter">
        <div class="icon">
          <Droplets size={24} strokeWidth={3} />
        </div>
        <h1>{plants.filter(plant => plant.rep >= daysBetween(new Date(), plant.last)).length}</h1>
    </div>
    <ul>
      {#each plants as plant}
        <li>{plant.name}</li>
      {/each}
    </ul>
    <div class="form">
      <button class="toggleButton" on:click={() => (openPlant = !openPlant)}>
        <span class="chevron" data-toggled={openPlant}>
          <ChevronDown />
        </span>
        <h2>Bæta við plöntu</h2>
      </button>
      {#if openPlant}
        <div transition:slide class="form__inputs">
          <label for="plant-name">Nafn</label>
          <input type="text" name="plant-name" />
          <label for="plant-rep">Vökva á...</label>
          <select placeholder="Water" name="plant-rep">
            <option value={Time.WEEK}>Viku fresti</option>
            <option value={Time.BIWEEK}>Tveggja vikna fresti</option>
            <option value={Time.MONTH}>Mánaðar fresti</option>
          </select>
          <label for="plant-last-watered">Vökvað síðast</label>
          <input type="date" name="plant-last-watered" />
          <button>Bæta við</button>
        </div>
      {/if}
    </div>
  </section>
</main>

<style>
  main {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 5rem;
    place-content: center;
  }

  section {
    background: #0002;
    border-radius: 1rem;
    padding: 1rem;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    height: fit-content;
  }

  .card_header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .card_counter {
    width: 3.5rem;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 0.5rem;
    border-radius: 0.5rem;
    background: #1a1a1a;
    position: relative;
    font-weight: bold;
    aspect-ratio: 1;

    .icon {
      position: absolute;
      top: -0.75rem;
      right: -0.75rem;
    }
  }

  .form {
    display: flex;
    justify-content: flex-start;
    flex-direction: column;
  }

  .form__inputs {
    display: flex;
    justify-content: flex-start;
    flex-direction: column;
    padding-top: 1rem;
    gap: 1rem;
  }

  .toggleButton {
    display: flex;
    justify-content: space-between;
    align-items: center;
    cursor: pointer;
  }

  .chevron {
    display: grid;
    place-content: center;
    transition: transform 0.3s;
  }

  [data-toggled="true"] {
    transform: rotate(180deg);
  }
</style>
