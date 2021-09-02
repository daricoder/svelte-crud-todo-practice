<script>
  import { onMount, afterUpdate } from "svelte";

  import { Toast } from "bootstrap";
  let toastEl;
  export let toastInfo;
  export let mostrarToast = false;

  $: toastInstance = new Toast(toastEl);

  afterUpdate(() => {
    console.log(mostrarToast);
    if (mostrarToast) {
      console.log('mostrando toast',toastEl);
      toastInstance.show();
      mostrarToast = false;
    }
  });
</script>

<div class="position-fixed bottom-0 end-0 p-3" style="z-index: 11">
  <div
    bind:this={toastEl}
    class="toast align-items-center text-white border-0 {toastInfo
      ? toastInfo.color
      : 'bg-success'}"
    role="alert"
    aria-live="assertive"
    aria-atomic="true"
  >
    <div class="d-flex">
      <div class="toast-body">{toastInfo ? toastInfo.texto : "prueba"}</div>
      <button
        type="button"
        class="btn-close btn-close-white me-2 m-auto"
        data-bs-dismiss="toast"
        aria-label="Close"
      />
    </div>
  </div>
</div>
