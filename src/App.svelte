<script>
  import { flip } from "svelte/animate";
  import { scale } from "svelte/transition";
  let todos = JSON.parse(localStorage.getItem("todos")) || [];
  let txtTodo = "";
  async function addTodo() {
    console.log("add todo");
    todos = [txtTodo, ...todos];
    txtTodo = "";
    localStorage.setItem("todos", JSON.stringify(todos));
  }
  async function removeTodo(index) {
    todos.splice(index, 1);
    todos = todos;
    localStorage.setItem("todos", JSON.stringify(todos));
  }
</script>

<main class="bg-blue-400 w-screen h-screen grid place-items-center ">
  <section
    class="bg-white h-screen w-full sm:h-5/6 sm:w-[500px] sm:rounded-xl py-8 px-2 flex flex-col space-y-4"
  >
    <h1 class="text-center text-xl tracking-wider">Todo App</h1>

    <form on:submit|preventDefault={addTodo} class="flex justify-between px-6">
      <input
        type="text"
        placeholder="Enter Todo..."
        bind:value={txtTodo}
        required
        class="rounded-lg py-2 px-4 flex-1 text-md"
      />
      <button type="submit" class="bg-blue-400 p-3 rounded-lg ml-4">➕</button>
    </form>

    <!-- <div class="outline-black flex-grow overflow-auto"> -->
    <ul class="flex-grow overflow-y-scroll">
      {#each todos as todo, index (todo)}
        <li
          transition:scale
          animate:flip
          class="flex items-end space-x-2 shadow p-3 rounded-xl mb-3 ml-6 mr-4"
        >
          <p class="flex-grow text-xl text-gray-700">{todo}</p>
          <button
            on:click={() => removeTodo(index)}
            class="bg-red-500 p-3 rounded-lg">🗑</button
          >
        </li>
      {:else}
        <div class="text-center text-lg my-8">You have no todos.</div>
      {/each}
    </ul>
    <!-- </div> -->
  </section>
</main>

<style>
  ::-webkit-scrollbar {
    /* height: 0.75rem; */
    width: 0.5rem;
  }
  ::-webkit-scrollbar-track {
    background-color: rgb(243, 244, 246);
    margin: 0 5rem 0 5rem;

    border-radius: 0.75rem;
  }
  ::-webkit-scrollbar-thumb {
    border-radius: 1vh;
    background-color: rgb(156, 163, 175);
  }
  ::-webkit-scrollbar-thumb:hover,
  ::-webkit-scrollbar-thumb:active {
    background-color: rgb(17, 24, 39);
  }
</style>
