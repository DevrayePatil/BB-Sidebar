<script>
  import { getContext } from "svelte"

  export let option1
  export let option2
  export let option3
  export let option4
  export let option5
  export let option6
  export let option7

  const { styleable } = getContext("sdk")
  const component = getContext("component")
</script>

<div use:styleable={$component.styles} class="side-bar">

  <div class="side-bar">
  <li class="list-style">
    <ul>{option1}</ul>
    <ul>{option2}</ul>
    <ul>{option3}</ul>
    <ul>{option4}</ul>
    <ul>{option5}</ul>
    <ul>{option6}</ul>
    <ul>{option7}</ul>
    <h1>hi</h1>
  </li>
  </div>
</div>


<style>
  div{
    padding: 0;
    margin: 0;
  }
  .side-bar{
    width: max-content;
    height: 100%;
    background-color: #fdd332;
  }

  .list-style{
    list-style: none;
    padding: 10px;
  }
</style>
