<script>

  export let todos;
  export let mostrarDialogo;
  let todo={};

  const addTodo = () => {
    if (todo.texto) {
      todo.texto.trim();
      todo.id = Date.now();
      todo.estado = false;
      todos = [...todos, todo];
      mostrarDialogo(todo.texto,'bg-primary');
      todo = {};
    }
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
  </div>
  
  