<script>
  import ChecklistItem from '../../components/ChecklistItem.svelte';

  let newItem = '';
  let checklist = JSON.parse(localStorage.getItem('checklist') || '[]');
  let index = Number
  function addItem() {
    if (newItem.trim()) {
      checklist = [...checklist, { text: newItem, done: false }];
      saveChecklist();
      newItem = '';
    }
  }

  function toggleDone(index) {
    checklist[index].done = !checklist[index].done;
    checklist = [...checklist];
    saveChecklist();
  }

  function deleteItem(index) {
    checklist.splice(index, 1);
    checklist = [...checklist]; // ← ini yang bikin Svelte sadar datanya berubah
    saveChecklist();
  }

  function saveChecklist() {
    localStorage.setItem('checklist', JSON.stringify(checklist));
  }
</script>

<main class="max-w-2xl mx-auto p-6 bg-white shadow-md rounded-md mt-6">
  <h1 class="text-3xl font-bold text-blue-700 mb-6">Checklist Hari Ini 📝</h1>

  <div class="flex items-center gap-2 mb-6">
    <input
      bind:value={newItem}
      placeholder="Tambahkan kegiatan..."
      class="flex-grow border border-blue-300 rounded-md p-2 focus:outline-none focus:ring-2 focus:ring-blue-400"
    />
    <button
      on:click={addItem}
      class="bg-blue-600 text-white px-4 py-2 rounded-md hover:bg-blue-700 transition"
    >
      Tambah
    </button>
  </div>

  <div class="space-y-3">
    {#each checklist as item, index}
      <ChecklistItem
        {item}
        on:toggle={() => toggleDone(index)}
        on:delete={() => deleteItem(index)}
    
      />
    {/each}

    {#if checklist.length === 0}
      <p class="text-gray-400 italic">Belum ada kegiatan. Tambahkan sesuatu yuk 🌱</p>
    {/if}
  </div>
</main>
