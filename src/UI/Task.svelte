<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();
  // your script goes here
  export let id;
  export let value = "New Task";
  export let firstCard = false;
  export let lastCard = false;
</script>

<style>
  /* your styles go here */
</style>

<label>
  <input
    type="text"
    placeholder="Insert task"
    bind:value
    on:blur={() => {
      dispatch('blurred', { value: value, id: id });
    }} />

  <button
    id="btnClose"
    on:click={() => {
      dispatch('deleteTask', (id = 2));
    }}>
    x
  </button>
  {#if !firstCard}
    <button
      id="moveLeft"
      on:click={() => {
        dispatch('moveLeft', (id = 2));
      }}>
      -
    </button>
  {/if}
  {#if !lastCard}
    <button
      id="moveRight"
      on:click={() => {
        dispatch('moveRight', (id = 2));
      }}>
      +
    </button>
  {/if}
</label>
