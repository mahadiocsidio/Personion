<script>
  export let item;
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();
</script>

<div class="flex items-center bg-blue-50 border border-blue-200 p-3 rounded-md shadow-sm">
  <input
    type="checkbox"
    checked={item.done}
    on:change={() => dispatch('toggle')}
    class="mr-3 w-5 h-5 text-blue-600 focus:ring-blue-500 border-gray-300 rounded"
  />
  <span class={`flex-grow text-base ${item.done ? 'line-through text-gray-400' : 'text-gray-800'}`}>
    {item.text}
  </span>
  <button
    on:click={() => dispatch('delete')}
    class="text-sm text-red-500 hover:underline ml-2"
  >
    Hapus
  </button>
</div>
