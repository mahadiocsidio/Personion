<script>
  import { onMount } from 'svelte';

  let today = new Date().toISOString().split('T')[0];
  let entry = '';

  function loadEntry() {
    const stored = JSON.parse(localStorage.getItem('diary') || '{}');
    entry = stored[today] || '';
  }

  function saveEntry() {
    const stored = JSON.parse(localStorage.getItem('diary') || '{}');
    stored[today] = entry;
    localStorage.setItem('diary', JSON.stringify(stored));
  }

  onMount(loadEntry);
</script>

<main class="p-4">
  <h1 class="text-2xl font-bold mb-2">Jurnal Refleksi Harian 📖</h1>
  <p class="mb-4 text-gray-600">Tanggal: {today}</p>

  <textarea
    bind:value={entry}
    class="w-full h-64 p-2 border rounded mb-4"
    placeholder="Tulis pikiranmu hari ini..."
  ></textarea>

  <button on:click={saveEntry} class="bg-blue-600 text-white px-4 py-2 rounded">
    Simpan
  </button>
</main>
