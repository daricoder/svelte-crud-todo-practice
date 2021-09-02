<script>

  import {onMount,afterUpdate} from 'svelte';
  import Toast from './components/Toast.svelte'
  import TodoList from './components/TodoList.svelte';
  import Form from './components/Form.svelte'
  let toastInfo;
  
  let todos = [];
  let mostrarToast;

  const mostrarDialogo=(texto,color)=>{
    toastInfo = {texto,color}
    mostrarToast=true;
  }
  
</script>
<Form bind:todos={todos} mostrarDialogo={mostrarDialogo}/>
<TodoList bind:todos={todos} mostrarDialogo={mostrarDialogo}/>
<Toast bind:mostrarToast={mostrarToast} toastInfo={toastInfo}/>

<style>
</style>
