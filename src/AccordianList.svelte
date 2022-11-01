<script>
  import { slide } from "svelte/transition";
  export let entry;
  let isOpen = false;
  const toggle = () => (isOpen = !isOpen);
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<div class="list-label" on:click={toggle} aria-expanded={isOpen}>
  <span style="backgound-color: red">{entry[0]}</span>
  <i class="expand-list-icon">
    <svg
      style="tran"
      width="15"
      height="15"
      fill="none"
      stroke-linecap="round"
      stroke-linejoin="round"
      stroke-width="3"
      viewBox="0 0 24 24"
      stroke="currentColor"><path d="M9 5l7 7-7 7" /></svg
    >
  </i>
</div>
{#if isOpen}
  <ul transition:slide={{ duration: 300 }}>
    {#each entry[1] as item}
      <li>{item}</li>
    {/each}
  </ul>
{/if}

<style>
  * {
    padding: 0;
  }

 

  ul {
    list-style: none;
    background-color: #fff;
  }
  ul li {
    padding: 2px;
    background-color: bisque;
    width: fit-content;
  }
  svg {
    transition: transform 0.2s ease-in;
  }

  .expand-list-icon {
    margin-top: 1px;
    float: right;
  }

  [aria-expanded="true"] svg {
    transform: rotate(0.25turn);
  }
</style>
