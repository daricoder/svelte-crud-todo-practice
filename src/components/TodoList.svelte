<script>
import Todo from './Todo.svelte';
export let todos = [];
export let mostrarDialogo;

const delTodo = (id) => {
    todos = todos.filter((todo) => todo.id != id);
    mostrarDialogo('Item Eliminado','bg-danger');
  };

  const editTodo = (id) => {
    let todo;
    todo = todos.find((todo) => todo.id === id);
    todo.estado = !todo.estado;
    todos = todos;
    mostrarDialogo('Item Editado','bg-warning');
  };

</script>


{#each todos as todo}
    <Todo todo={todo} editTodo={editTodo} delTodo={delTodo} />
{/each}

