<script>
  import { createEventDispatcher } from "svelte";
  let fire = createEventDispatcher();
  let confirm = false;

  function confirmDelete() {
    confirm = true;
  }

  function cancelConfirm() {
    confirm = false;
  }

  function confirmed(event) {
    confirm = false;
    fire("delete", event);
  }
</script>

{#if confirm}
  <button
    type="button"
    on:click={(event) => cancelConfirm()}
    class="btn btn-success ">Cancel</button
  >
  <button type="button" on:click={(event) => confirmed()} class="btn btn-danger"
    >Sure?</button
  >
{:else}
  <button
    type="button"
    on:click={(event) => confirmDelete(event)}
    class="btn btn-danger btn-sm"
  >
    <b>x</b>
  </button>
{/if}
