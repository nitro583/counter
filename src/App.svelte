<script lang="ts">
  // import { current_component, prevent_default } from "svelte/internal";

  let counters: { name: string; count: number }[] = [
    {
      name: "new",
      count: 0,
    },
  ];
	let totalCount:number;
	$: totalCount = counters.reduce((prev, current) => prev + current.count, 0);
	
  const countUp = (index: number) => {
    counters[index].count += 1;
  };
  const countDown = (index: number) => {
    counters[index].count += -1;
  };
  const resetCount = (index: number) => {
    counters[index].count = 0;
  };
  const createCounter = () => {
    counters = [
      ...counters,
      {
        name: "new",
        count: 0,
      },
    ];
    counters = counters;
  };
  const deleteCounter = (index: number) => {
    counters.splice(index, 1);
    counters = counters;
  };
</script>

<h1>Multiple Counter</h1>
<div class="wrapper">
  {#each counters as counter, index}
    <div class="counter">
      <input type="text" bind:value={counter.name} />
      <p class="counter-count">
        {counter.count}
      </p>

      <button class="button-countup" on:click={() => countUp(index)}> +</button>
      {#if counter.count <= 0}
        <button class="button-countdown">-</button>
      {:else}
        <button class="button-countdown" on:click={() => countDown(index)}
          >-</button
        >
      {/if}
      <button class="button-reset" on:click={() => resetCount(index)}>0</button>
      <button class="button-delete" on:click={() => deleteCounter(index)}
        >X</button
      >
    </div>
  {/each}
  <button class="button-create" on:click={createCounter}>Create Counter</button>
  <p>
    title list:
    {#each counters as counter, index}
      {#if index + 1 === counters.length}
        {" " + counter.name}
      {:else}
        {" " + counter.name + ","}
      {/if}
    {/each}
  </p>
  <p>
    sum of count: {totalCount}
  </p>
</div>

<style>
  h1 {
    text-align: center;
    font-size: 45px;
  }
  p {
    text-align: center;
  }
  .wrapper {
    width: 600px;
    max-width: 90%;
    margin: auto;
  }
  .counter {
    background: #ececec;
    padding: 10px;
    border-radius: 5px;
    filter: drop-shadow(2px 2px 2px rgba(0, 0, 0, 0.2));
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 10px auto;
  }
  input {
    margin: 0 10px;
    width: 30%;
    border-radius: 5px;
    border: none;
  }
  .counter-count {
    width: 30%;
    font-size: 20px;
    line-height: 20px;
    margin: 0;
    font-weight: bold;
    text-align: center;
  }

  button {
    width: 10%;
    margin: 0;
    border: none;
  }
  .button-countup {
    background-color: #f56565;
    color: #fff;
    border-radius: 5px 0 0 5px;
  }
  .button-countdown {
    background-color: #4299e1;
    color: #fff;
    border-radius: 0;
  }
  .button-reset {
    background-color: #ecc94b;
    color: #fff;
    border-radius: 0 5px 5px 0;
  }
  .button-delete {
    background-color: inherit;
    color: #333;
  }
  .button-create {
    width: 100%;
    border-radius: 5px;
    background-color: #d8ece2;
    border: none;
    filter: drop-shadow(2px 2px 2px rgba(0, 0, 0, 0.2));
  }
</style>
