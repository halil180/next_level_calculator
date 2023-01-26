<script lang="ts">
	import { fade } from 'svelte/transition';
  import * as math from "mathjs";
  let expression: string = "";
  let result: string = "";
  let timerId: any;
  let activeButton: string = "";
  $: try {
    if (timerId) clearTimeout(timerId);
    result = math.evaluate(expression);
  } catch (e) {
    // delay showing error message by 1,2 second
    timerId = setTimeout(() => {
      result = "Invalid Expression";
    }, 1000);
  }
  const handleClick = (event: Event) => {
    const target = event.target as HTMLButtonElement;
    expression += target.innerText;
  };
  document.addEventListener("keydown", function (event) {
    if (event.key === "0") {
      activeButton = "0";
      expression += "0";
    }
    if (event.key === "1") {
      activeButton = "1";
      expression += "1";
    }
    if (event.key === "2") {
      activeButton = "2";
      expression += "2";
    }
    if (event.key === "3") {
      activeButton = "3";
      expression += "3";
    }
    if (event.key === "4") {
      activeButton = "4";
      expression += "4";
    }
    if (event.key === "5") {
      activeButton = "5";
      expression += "5";
    }
    if (event.key === "6") {
      activeButton = "6";
      expression += "6";
    }
    if (event.key === "7") {
      activeButton = "7";
      expression += "7";
    }
    if (event.key === "8") {
      activeButton = "8";
      expression += "8";
    }
    if (event.key === "9") {
      activeButton = "9";
      expression += "9";
    }
    if (event.key === "-") {
      activeButton = "-";
      expression += "-";
    }
    if (event.key === "+") {
      activeButton = "+";
      expression += "+";
    }
    if (event.key === "/") {
      activeButton = "/";
      expression += "/";
    }
    if (event.key === ".") {
      activeButton = ".";
      expression += ".";
    }
    if (event.key === "*") {
      activeButton = "*";
      expression += "*";
    }
    if (event.key === "Backspace" || event.key === "Delete") {
      expression = expression.slice(0, -1);
      activeButton = "Delete";
    }
    if (event.key === "(") {
      activeButton = "(";
      expression += "(";
    }
    if (event.key === ")") {
      activeButton = ")";
      expression += ")";
    }
  });
  document.addEventListener("keyup", () => {
    activeButton = "";
  });
</script>

<main class="flex items-center justify-center h-screen flex-col ">
  <div class=" rounded p-4 border">
    {#if result}
      <h1 class="text-center my-4 text-3xl  bg-primary rounded "   in:fade={{duration: 300}}
      out:fade={{duration: 300}}> {result}</h1>
      
    {/if}
    <input
      type="text"
      class="input input-ghost w-full max-w-xs mb-5"
      bind:value={expression}
      readonly
    />
    <div class="grid grid-cols-4 gap-4">
      <button
        class="btn lg:btn-lg"
        class:btn-primary={activeButton === "7"}
        on:click={handleClick}>7</button
      >
      <button
        class="btn lg:btn-lg"
        class:btn-primary={activeButton === "8"}
        on:click={handleClick}>8</button
      >
      <button
        class="btn lg:btn-lg"
        class:btn-primary={activeButton === "9"}
        on:click={handleClick}>9</button
      >
      <button
        class="btn glass lg:btn-lg"
        class:btn-primary={activeButton === "/"}
        on:click={handleClick}>/</button
      >
      <button
        class="btn lg:btn-lg"
        class:btn-primary={activeButton === "4"}
        on:click={handleClick}>4</button
      >
      <button
        class="btn lg:btn-lg"
        class:btn-primary={activeButton === "5"}
        on:click={handleClick}>5</button
      >
      <button
        class="btn lg:btn-lg "
        class:btn-primary={activeButton === "6"}
        on:click={handleClick}>6</button
      >
      <button
        class="btn  glass lg:btn-lg"
        class:btn-primary={activeButton === "*"}
        on:click={handleClick}>*</button
      >
      <button
        class="btn  lg:btn-lg"
        class:btn-primary={activeButton === "1"}
        on:click={handleClick}>1</button
      >
      <button
        class="btn lg:btn-lg "
        class:btn-primary={activeButton === "2"}
        on:click={handleClick}>2</button
      >
      <button
        class="btn lg:btn-lg"
        class:btn-primary={activeButton === "3"}
        on:click={handleClick}>3</button
      >
      <button
        class="btn glass lg:btn-lg"
        class:btn-primary={activeButton === "-"}
        on:click={handleClick}>-</button
      >
      <button
        class="btn lg:btn-lg"
        class:btn-primary={activeButton === "0"}
        on:click={handleClick}>0</button
      >
      <button
        class="btn lg:btn-lg"
        class:btn-primary={activeButton === "."}
        on:click={handleClick}>.</button
      >
      <button
        class="btn btn-error  lg:btn-lg"
        class:btn-ghost={activeButton === "Delete"}
        on:click={() => (expression = expression.slice(0, -1))}>EC</button
      >
      <button
        class="btn glass lg:btn-lg"
        class:btn-primary={activeButton === "+"}
        on:click={handleClick}>+</button
      >
    </div>
  </div>
</main>
<style>
  input:focus {
  border: none !important;
  
}

</style>