<script>
  import Icons from "./icons.svelte";

  let newItem = "";
  let todoList = [];

  function addToList() {
    if (newItem !== "") {
      todoList = [
        ...todoList,
        {
          text: newItem,
          completed: false,
        },
      ];
      newItem = "";
    }
  }

  function removeFromList(index) {
    todoList.splice(index, 1);
    todoList = todoList;
  }
</script>

<main class="container">
  <div class="todos_container">
    <form on:submit|preventDefault={addToList} class="">
      <input
        bind:value={newItem}
        type="text"
        class="todos__input"
        placeholder="Enter Todo"
      />
      <button class="todos__button">+</button>

      <h2 class="todos__listHeader">
        <center>Todos</center>
      </h2>

      <div class="todos">
        {#each todoList as item, index}
          <div class="todo">
            <span
              class={`todo__text ${
                item.completed ? "todo__checked--strike" : ""
              }`}>{item.text}</span
            >

            <div class="icons">
              <button
                class="icon__button"
                on:click={() => (item.completed = !item.completed)}
              >
                <Icons name="save" class="icon" />
              </button>

              <button
                class="icon__button"
                on:click={() => removeFromList(index)}
              >
                <Icons name="trash" class="icon" />
              </button>
            </div>
          </div>
        {/each}
      </div>
    </form>
  </div>
</main>

<style>
  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
    min-height: 100vh;
    background: #222e50
      url(https://images.unsplash.com/photo-1579546929518-9e396f3cc809?ixid=MXwxMjA3fDB8MHxzZWFyY2h8N3x8Z3JhZGllbnR8ZW58MHx8MHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60)
      top center repeat;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: 50%;
  }

  .todos_container {
    margin-top: 10%;
  }

  .todo {
    display: flex;
    padding: 20px;
    border-radius: 20px;
    box-shadow: 0 0 15px rgb(0 0 0 / 20%);
    background-color: hsla(0, 0%, 100%, 0.1);
    -webkit-backdrop-filter: blur(25px);
    backdrop-filter: blur(25px);
    width: inherit;
    margin-top: 15px;
    font-size: 1.2rem;
    justify-content: space-between;
    align-items: center;
  }

  .todos__listHeader {
    align-items: center;
    justify-content: center;
    padding: 20px;
    border-radius: 20px;
    box-shadow: 0 0 15px rgb(0 0 0 / 20%);
    background-color: hsla(0, 0%, 100%, 0.1);
    -webkit-backdrop-filter: blur(25px);
    backdrop-filter: blur(25px);
    margin-top: 15px;
    font-size: 1.2rem;
  }

  .todos__input {
    background-color: inherit;
    border: none;
    box-shadow: none;
    text-decoration: none;
    font-size: 1.2rem;
    border-bottom: 1px solid black;
    margin-top: 15px;
    outline: none;
    width: 500px;
  }

  .todos__button {
    background-color: inherit;
    border: none;
    box-shadow: none;
    font-size: 1.2rem;
    cursor: pointer;
  }

  .todo__checked--strike {
    text-decoration: line-through;
  }

  .icon__button {
    background-color: transparent;
    border: none;
    box-shadow: none;
    font-size: 1.2rem;
    cursor: pointer;
    color: rgba(0, 0, 0, 0.54);
  }

  .icon {
    background: rgba(0, 0, 0, 0.54);
  }
</style>
