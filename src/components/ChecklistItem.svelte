<script>
  export let item;
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();
</script>

<div class="flex items-center mb-2">
  <input
    type="checkbox"
    checked={item.done}
    on:change={() => dispatch('toggle')}
    class="mr-2"
  />
  <span class={item.done ? 'line-through text-gray-500' : ''}>{item.text}</span>
  <button on:click={() => dispatch('delete')} class="ml-auto text-red-500 hover:underline text-sm">
    Hapus
  </button>
</div>
