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
  export let option1Link, option2Link, option4Link, option5Link;

  export let subOption1Link1, subOption1Link2, subOption1Link3;
  export let subOption2Link1, subOption2Link2;
  export let subOption3Link1, subOption3Link2, subOption3Link3, subOption3Link4;

  const { styleable } = getContext("sdk");
  const component = getContext("component");

  const subListData = {
    Estimation: [
      ["Estimation Breakup", subOption1Link1],
      ["Estimation Summery", subOption1Link2],
      ["Estimation Revision", subOption1Link3],
    ],
    Costing: [
      ["Cost Variation", subOption2Link1],
      ["Cost Breakup", subOption2Link2],
    ],
    Resources: [
      ["Material", subOption3Link1],
      ["Labour", subOption3Link2],
      ["Machinery & Equipments", subOption3Link3],
      ["Material + Labour", subOption3Link4],
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
          </span><a href={option1Link} rel="noreferrer">{option1}</a>
        </li>
        <li>
          <span class="list-icon">
            <Icon data={projectLibraryIcon} />
          </span><a href={option2Link} rel="noreferrer">{option2}</a>
        </li>
        <li class="expand-list">
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
          </span><a href={option4Link} rel="noreferrer">{option4}</a>
        </li>
        <li>
          <span class="list-icon">
            <Icon data={projectUsers} />
          </span><a href={option5Link} rel="noreferrer">{option5}</a>
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
  .side-bar {
    width: max-content;
    height: 100%;
    background-color: var(--bg-color, rgba(255, 255, 255, 0));
    position: sticky;
  }

  .list-style {
    padding: 10px;
  }
  .list-style ul {
    list-style: none;
  }
  .list-style ul li {
    padding: 5px 10px;
    color: #000;
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

  svg {
    transition: transform 0.2s ease-in;
  }

  [aria-expanded="true"] svg {
    transform: rotate(0.25turn);
  }
</style>
