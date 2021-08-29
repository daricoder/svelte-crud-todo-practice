<script>
  import { Toast } from "bootstrap";
  let toastEl;
  let toastInstance;
  let toastColor;
  let todos = [];
  let todo = {};

  $: if (toastEl) {
    if (!toastInstance) {
      toastInstance = new Toast(toastEl);
      console.log("instance");
    } else {
      toastInstance.show();
      console.log("updte toastEl");
      console.log(toastEl);
    }
  }

  const addTodo = () => {
    if (todo.texto) {
      todo.texto.trim();
      todo.id = Date.now();
      todo.estado = false;
      todos = [...todos, todo];
      todo = {};
      toastColor = "primary";
      toastEl = toastEl;
    }
  };

  const delTodo = (id) => {
    todos = todos.filter((todo) => todo.id != id);
    toastColor = "danger";
    toastinstance.show();
  };

  const editTodo = (id) => {
    let todo;
    todo = todos.find((todo) => todo.id === id);
    todo.estado = !todo.estado;
    todos = todos;
    toastColor = "success";
    toastInstance.show();
    //   console.log(todos);
    //   todos=todos;
  };
</script>

<div class="container">
  <h1 class="display-5" my-3>CRUD</h1>
  <form on:submit|preventDefault={addTodo}>
    <input
      type="text"
      placeholder="Enter para agregar todo"
      class="form-control shadow border-0"
      bind:value={todo.texto}
    />
  </form>
  {#each todos as todo}
    <div class="shadow my-3 p-3 lead">
      <p class={todo.estado ? "text-decoration-line-through" : ""}>
        {todo.texto}
      </p>
      <button
        class="btn btn-sm btn-{todo.estado ? 'warning' : 'primary'}"
        on:click={editTodo(todo.id)}
        ><i
          class={todo.estado ? "bi bi-arrow-clockwise" : "bi bi-check2"}
        /></button
      >
      <button class="btn btn-sm btn-danger" on:click={delTodo(todo.id)}
        ><i class="bi bi-trash" /></button
      >
    </div>
  {/each}
</div>

<div
  bind:this={toastEl}
  class="toast align-items-center text-white bg-{toastColor} border-0"
  role="alert"
  aria-live="assertive"
  aria-atomic="true"
>
  <div class="d-flex">
    <div class="toast-body">Hello, world! This is a toast message.</div>
    <button
      type="button"
      class="btn-close btn-close-white me-2 m-auto"
      data-bs-dismiss="toast"
      aria-label="Close"
    />
  </div>
</div>

<style>
</style>
