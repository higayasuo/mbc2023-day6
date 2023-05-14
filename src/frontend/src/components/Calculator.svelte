<script>
  import { onMount } from "svelte";
  import { auth } from "../store/auth";

  let counter = "0";

  let addArg1 = "1";
  let addResult = "";

  let subArg1 = "1";
  let subResult = "";

  let mulArg1 = "2";
  let mulResult = "";

  let divArg1 = "2";
  let divResult = "";

  let resetResult = "";

  let powerArg1 = "2";
  let powerResult = "";

  let sqrtResult = "";

  let floorResult = "";

  onMount(async () => {
    counter = await $auth.actor.see();
  });

  async function addClick() {
    addResult = await $auth.actor.add(Number(addArg1));
    counter = addResult;
  }

  async function subClick() {
    subResult = await $auth.actor.sub(Number(subArg1));
    counter = subResult;
  }

  async function mulClick() {
    mulResult = await $auth.actor.mul(Number(mulArg1));
    counter = mulResult;
  }

  async function divClick() {
    const arg1Num = Number(divArg1);
    divResult = await $auth.actor.div(arg1Num);
    if (arg1Num != 0) {
      counter = divResult;
    }
  }

  async function resetClick() {
    await $auth.actor.reset();
    resetResult = await $auth.actor.see();
    counter = resetResult;
  }

  async function powerClick() {
    powerResult = await $auth.actor.power(Number(powerArg1));
    counter = powerResult;
  }

  async function sqrtClick() {
    sqrtResult = await $auth.actor.sqrt();
    counter = sqrtResult;
  }

  async function floorClick() {
    floorResult = await $auth.actor.floor();
    counter = floorResult;
  }
</script>

{#if $auth.loggedIn}
  <div class="container">
    <div>counter: {counter}</div>
    <div class="calc">
      <input type="text" bind:value={addArg1} class="num" />
      <button on:click={addClick} class="calcButtn"> Add </button>
      <span class="result">{addResult}</span>
    </div>

    <div class="calc">
      <input type="text" bind:value={subArg1} class="num" />
      <button on:click={subClick} class="calcButtn"> Sub </button>
      <span class="result">{subResult}</span>
    </div>

    <div class="calc">
      <input type="text" bind:value={mulArg1} class="num" />
      <button on:click={mulClick} class="calcButtn"> Mul </button>
      <span class="result">{mulResult}</span>
    </div>

    <div class="calc">
      <input type="text" bind:value={divArg1} class="num" />
      <button on:click={divClick} class="calcButtn"> Div </button>
      <span class="result">{divResult}</span>
    </div>

    <div class="calc">
      <input type="text" class="hide" />
      <button on:click={resetClick} class="calcButtn"> Reset </button>
      <span class="result">{resetResult}</span>
    </div>

    <div class="calc">
      <input type="text" bind:value={powerArg1} class="num" />
      <button on:click={powerClick} class="calcButtn"> Power </button>
      <span class="result">{powerResult}</span>
    </div>

    <div class="calc">
      <input type="text" class="hide" />
      <button on:click={sqrtClick} class="calcButtn"> Sqrt </button>
      <span class="result">{sqrtResult}</span>
    </div>

    <div class="calc">
      <input type="text" class="hide" />
      <button on:click={floorClick} class="calcButtn"> Floor </button>
      <span class="result">{floorResult}</span>
    </div>
  </div>
{/if}

<style>
  .container {
    margin: 64px 0;
  }
  .num {
    text-align: right;
  }
  .result {
    display: inline-block;
    width: 30px;
    text-align: right;
  }
  .calc {
    margin-top: 10px;
  }
  .calcButtn {
    width: 100px;
    text-align: center;
  }
  .hide {
    visibility: hidden;
  }
</style>
