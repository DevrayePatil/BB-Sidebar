<script>
  import { getContext } from "svelte";
  import Icon from "svelte-icon";

  import costSummeryIcon from "./resources/cost-summary-dollar.svg";
  import projectLibraryIcon from "./resources/cost-library.svg";
  import reportIcon from "./resources/report.svg";
  // import projectDetailsIcon from "./resources/details.htm";
  import projectUsers from "./resources/users.svg";

  import dropdownIcon from "./resources/dropdown-icon.svg";

  import { slide } from "svelte/transition";
  import AccordianList from "./AccordianList.svelte";

  export let backgroundColor;
  export let option1, option2, option3, option4, option5;

  const { styleable } = getContext("sdk");
  const component = getContext("component");

  const subListData = {
    Estimation: [
      "Estimation Breakup",
      "Estimation Summery",
      "Estimation Revision",
    ],
    Costing: ["Cost Variation", "Cost Breakup"],
    Resources: [
      "Material",
      "Labour",
      "Machinery & Equipments",
      "Material + Labour",
    ],
  };

  const listData = ["Estimation", "Costing", "Resources"];

  let isOpen = false;
  const toggle = () => (isOpen = !isOpen);
</script>

<div use:styleable={$component.styles} class="side-bar">
  <div class="side-bar" style="--bg-color: {backgroundColor}">
    <div class="list-style">
      <ul>
        <li>
          <span class="list-icon">
            <Icon data={costSummeryIcon} />
          </span>{option1}
        </li>
        <li>
          <span class="list-icon">
            <Icon data={projectLibraryIcon} />
          </span>{option2}
        </li>
        <li class="expand-list" >
          <!-- svelte-ignore a11y-click-events-have-key-events -->
          <div on:click={toggle} aria-expanded={isOpen}>
          <span class="list-icon">
            <Icon data={reportIcon} />
          </span>{option3}
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

          <div class="expanded-list" transition:slide={{ duration: 300 }}>
            <ul>
              {#each Object.entries(subListData) as entry}
                <AccordianList {entry} />
              {/each}

            </ul>
          </div>
          {/if}

        </li>
        <li>
          <span class="list-icon">
            <Icon data={costSummeryIcon} />
          </span>{option4}
        </li>
        <li>
          <span class="list-icon">
            <Icon data={projectUsers} />
          </span>{option5}
        </li>
      </ul>
    </div>
  </div>
</div>

<style>
  * {
    padding: 0;
    margin: 0;
  }
  span {
    vertical-align: middle;
  }
  .side-bar {
    width: max-content;
    height: 100%;
    background-color: var(--bg-color, rgba(255, 255, 255, 0));
  }

  .list-style {
    padding: 10px;
  }
  .list-style ul {
    list-style: none;
  }
  .list-style ul li {
    padding: 5px 10px;
  }
  .list-style ul li:hover {
    background-color: rgba(0, 100, 255, 0.1);
    cursor: pointer;
  }
  .list-icon {
    margin-right: 10px;
  }
  .expand-list-icon {
    float: right;
    margin-top: 5px;
  }



  .expand-list:hover .list-icon {
    transform: rotate(-90deg);
    -webkit-transform: rotate(-90deg);
  }

  .expand-list-icon {
    margin-top: 2px;
    float: right;
    
  }

  [aria-expanded="true"] svg {
    transform: rotate(0.25turn);
  }
</style>
