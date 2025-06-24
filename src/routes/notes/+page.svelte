<script>
  import ChecklistItem from '../../components/ChecklistItem.svelte';
  let index = Number
  let newItem = '';
  let checklist = JSON.parse(localStorage.getItem('checklist') || '[]');

  function addItem() {
    if (newItem.trim()) {
      checklist = [...checklist, { text: newItem, done: false }];
      saveChecklist();
      newItem = '';
    }
  }

  function toggleDone(index) {
    checklist[index].done = !checklist[index].done;
    saveChecklist();
  }

  function deleteItem(index) {
  checklist = checklist.filter((_, i) => i !== index);
  saveChecklist();
    }


  function saveChecklist() {
    localStorage.setItem('checklist', JSON.stringify(checklist));
  }
</script>

<main class="p-4">
  <h1 class="text-2xl font-bold mb-4">Checklist Hari Ini 📝</h1>

  <div class="mb-4">
    <input
      bind:value={newItem}
      placeholder="Tambahkan kegiatan..."
      class="border rounded p-2 mr-2"
      on:keydown={(e) => e.key === 'Enter' && addItem()}
    />
    <button on:click={addItem} class="bg-green-600 text-white px-4 py-2 rounded">Tambah</button>
  </div>

  {#each checklist as item, index}
    <ChecklistItem {item} on:toggle={() => toggleDone(index)} on:delete={() => deleteItem(index)} />
  {/each}

  {#if checklist.length === 0}
    <p class="text-gray-500">Belum ada kegiatan. Yuk, tambahkan sesuatu!</p>
  {/if}
</main>
