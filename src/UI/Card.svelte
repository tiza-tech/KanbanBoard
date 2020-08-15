<script>
  // your script goes here
  import { createEventDispatcher } from "svelte";
  import { empty } from "svelte/internal";
  const dispatch = createEventDispatcher();
  let largeTexts = true;
  export let id;
  export let title;
  export let newCard;
</script>

<style>
  card {
    padding: 0.5rem 1rem;
    margin: 1rem;
    /* box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0, 2);  this style is invalide in svelte*/
    transition: 0.3s;
    border-color: #ccc;
    border-style: solid;
    border-radius: 10px;
    width: 20%;
  }
  h3 {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  button {
    top: 0.5rem;
    right: 0.5rem;
    padding: 0 0.4rem;
    color: rgb(167, 0, 0);
    background-color: #f4f4f4;
    border: none;
    visibility: hidden;
  }

  button:not(:disabled):active {
    background-color: rgb(167, 0, 0);
    color: #f4f4f4;
  }

  h3:hover button {
    visibility: visible;
  }
</style>

<card {id} class:newCard>
  <h3 class:newCardTitl={newCard}>
    {#if !title}card is empty{:else}{title}{/if}

    <button
      on:click={() => {
        dispatch('deleteCard', (id = 1));
      }}>
      x
    </button>
  </h3>
  <slot>Empty Card</slot>
</card>
