<script>
    export let todo={id:Date.now(),texto:'prueba',estado:false};
    export let editTodo;
    export let delTodo;
</script>


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