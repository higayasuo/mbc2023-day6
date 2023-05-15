<script>
  import { onMount } from "svelte";
  import { auth } from "../store/auth";

  const REQUIRED_ERROR = "Required";
  const NEGATIVE_NUMBER_ERROR = "Negative number";
  const NEGATIVE_RESULT_ERROR = "Negative result";
  const ZERO_DIVISION_ERROR = "Zero division";

  let counter = "0";

  let addArg1 = "1";
  let subArg1 = "1";
  let mulArg1 = "2";
  let divArg1 = "2";
  let powerArg1 = "2";

  let addError = "";
  let subError = "";
  let mulError = "";
  let divError = "";
  let powerError = "";

  onMount(async () => {
    counter = await $auth.actor.see();
  });

  function clearErrors() {
    addError = "";
    subError = "";
    mulError = "";
    divError = "";
    powerError = "";
  }

  async function addClick() {
    clearErrors();
    if (addArg1 === null || addArg1 === "") {
      addError = REQUIRED_ERROR;
      return;
    }
    const num = Number(addArg1);
    if (num < 0) {
      addError = NEGATIVE_NUMBER_ERROR;
      return;
    }

    counter = await $auth.actor.add(num);
  }

  async function subClick() {
    clearErrors();
    if (subArg1 === null || subArg1 === "") {
      subError = REQUIRED_ERROR;
      return;
    }
    const num = Number(subArg1);
    if (num < 0) {
      subError = NEGATIVE_NUMBER_ERROR;
      return;
    }
    if (counter - num < 0) {
      subError = NEGATIVE_RESULT_ERROR;
      return;
    }

    counter = await $auth.actor.sub(num);
  }

  async function mulClick() {
    clearErrors();
    if (mulArg1 === null || mulArg1 === "") {
      mulError = REQUIRED_ERROR;
      return;
    }
    const num = Number(mulArg1);
    if (num < 0) {
      mulError = NEGATIVE_NUMBER_ERROR;
      return;
    }

    counter = await $auth.actor.mul(num);
  }

  async function divClick() {
    clearErrors();
    if (divArg1 === null || divArg1 === "") {
      divError = REQUIRED_ERROR;
      return;
    }
    const num = Number(divArg1);
    if (num < 0) {
      divError = NEGATIVE_NUMBER_ERROR;
      return;
    }
    if (num == 0) {
      divError = ZERO_DIVISION_ERROR;
      return;
    }

    counter = await $auth.actor.div(num);
  }

  async function resetClick() {
    clearErrors();
    await $auth.actor.reset();
    counter = await $auth.actor.see();
  }

  async function powerClick() {
    clearErrors();
    if (powerArg1 === null || powerArg1 === "") {
      powerError = REQUIRED_ERROR;
      return;
    }
    const num = Number(powerArg1);
    if (num < 0) {
      powerError = NEGATIVE_NUMBER_ERROR;
      return;
    }

    counter = await $auth.actor.power(num);
  }

  async function sqrtClick() {
    clearErrors();
    counter = await $auth.actor.sqrt();
  }

  async function floorClick() {
    clearErrors();
    counter = await $auth.actor.floor();
  }
</script>

{#if $auth.loggedIn}
  <div class="container">
    <div class="counter">Counter: {counter}</div>
    <div class="calc">
      <input type="number" min="0" bind:value={addArg1} class="num" />
      <button on:click={addClick} class="calcButtn"> Add </button>
      <span class="error">{addError}</span>
    </div>

    <div class="calc">
      <input type="number" min="0" bind:value={subArg1} class="num" />
      <button on:click={subClick} class="calcButtn"> Sub </button>
      <span class="error">{subError}</span>
    </div>

    <div class="calc">
      <input type="number" min="0" bind:value={mulArg1} class="num" />
      <button on:click={mulClick} class="calcButtn"> Mul </button>
      <span class="error">{mulError}</span>
    </div>

    <div class="calc">
      <input type="number" min="1" bind:value={divArg1} class="num" />
      <button on:click={divClick} class="calcButtn"> Div </button>
      <span class="error">{divError}</span>
    </div>

    <div class="calc">
      <input type="number" class="hideNum" />
      <button on:click={resetClick} class="calcButtn"> Reset </button>
      <span class="error">{""}</span>
    </div>

    <div class="calc">
      <input type="number" min="0" bind:value={powerArg1} class="num" />
      <button on:click={powerClick} class="calcButtn"> Power </button>
      <span class="error">{powerError}</span>
    </div>

    <div class="calc">
      <input type="number" class="hideNum" />
      <button on:click={sqrtClick} class="calcButtn"> Sqrt </button>
      <span class="error">{""}</span>
    </div>

    <div class="calc">
      <input type="number" class="hideNum" />
      <button on:click={floorClick} class="calcButtn"> Floor </button>
      <span class="error">{""}</span>
    </div>
  </div>
{/if}

<style>
  .container {
  }
  .counter {
    width: 200px;
    height: 30px;
    padding: 0;
    text-align: center;
    position: relative;
    display: inline-block;
    padding: 0.25em 0.5em;
    text-decoration: none;
    font-size: x-large;
  }
  .num {
    display: inline-block;
    width: 200px;
    text-align: right;
    border-radius: 6px;
  }
  .error {
    display: inline-block;
    width: 200px;
    text-align: left;
    margin-left: 10px;
    color: red;
  }
  .calc {
    margin: 10px;
    padding-left: auto;
    padding-right: auto;
  }
  .calcButtn {
    width: 70px;
    height: 30px;
    padding: 0;
    text-align: center;
    position: relative;
    display: inline-block;
    padding: 0.25em 0.5em;
    text-decoration: none;
    color: #fff;
    background: #fd9535; /*背景色*/
    border-bottom: solid 2px #d27d00; /*少し濃い目の色に*/
    border-radius: 4px; /*角の丸み*/
    box-shadow: inset 0 2px 0 rgba(255, 255, 255, 0.2),
      0 2px 2px rgba(0, 0, 0, 0.19);
    font-weight: bold;
  }
  .calcButtn:hover {
    background: #f3aa66;
  }
  .calcButtn:active {
    border-bottom: solid 5px #fd9535;
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.3);
  }
  .hideNum {
    display: inline-block;
    width: 200px;
    visibility: hidden;
  }
</style>
