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
      <li><a href={item[1]}>{item[0]}</a></li>
    {/each}
  </ul>
{/if}

<style>
  * {
    padding: 0;
  }
  a:link,
  a:visited {
    color: black;
    text-align: center;
    text-decoration: none;
    display: inline-block;
  }

  a:hover,
  a:active {
    cursor: pointer;
  }
 

  ul {
    list-style: none;
  }
  ul li {
    padding: 2px;
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
