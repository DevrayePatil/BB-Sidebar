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
    <ul class="list-item">{option1}</ul>
    <ul class="list-item">{option2}</ul>
    <ul class="list-item">{option3}</ul>
    <ul class="list-item">{option4}</ul>
    <ul class="list-item">{option5}</ul>
    <ul class="list-item">{option6}</ul>
    <ul class="list-item">{option7}</ul>
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
    background-color: white;
  }

  .list-style{
    list-style: none;
    padding: 10px;
  }

  .list-item{
    padding: 5px;
    margin: 3px;
  }
</style>
