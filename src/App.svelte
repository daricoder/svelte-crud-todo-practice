<script>

  import {onMount,afterUpdate} from 'svelte';
  import {Toast} from 'bootstrap'
  let todos = [];
  let todo = {};
  let mostrarToast=false;
  let toastEl;
  // let toastInstance;
  let toastInfo;

  $: toastInstance = new Toast(toastEl);

  const addTodo = () => {
    if (todo.texto) {
      todo.texto.trim();
      todo.id = Date.now();
      todo.estado = false;
      todos = [...todos, todo];
      toastInfo = {texto: todo.texto,color:'bg-primary'};
      todo = {};
      toastEl = toastEl;
      mostrarToast=true;

    }
  };

  const delTodo = (id) => {
    todos = todos.filter((todo) => todo.id != id);
    toastInfo = {texto: 'Item Eliminado',color:'bg-danger'};
    mostrarToast=true;
  };

  const editTodo = (id) => {
    let todo;
    todo = todos.find((todo) => todo.id === id);
    todo.estado = !todo.estado;
    todos = todos;
    toastInfo = {texto: 'Item Editado',color:'bg-warning'};
    mostrarToast=true;
  };

  afterUpdate(()=>{
    if(mostrarToast){
      toastInstance.show();
      mostrarToast = false;
    }
  });
  
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

<div class="position-fixed bottom-0 end-0 p-3" style="z-index: 11">
  <div
    bind:this={toastEl}
    class="toast align-items-center text-white border-0 {toastInfo ? toastInfo.color: 'bg-sucess'}"
    role="alert"
    aria-live="assertive"
    aria-atomic="true"
  >
    <div class="d-flex">
      <div class="toast-body">{toastInfo ? toastInfo.texto: 'prueba'}</div>
      <button
        type="button"
        class="btn-close btn-close-white me-2 m-auto"
        data-bs-dismiss="toast"
        aria-label="Close"
      />
    </div>
  </div>
</div>


<style>
</style>
