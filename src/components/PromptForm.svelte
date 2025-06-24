<script>
  import PromptForm from '../components/PromptForm.svelte';

  let dailyPrompt = localStorage.getItem("dailyPrompt") || "";
</script>

<main class="p-4">
  <h1 class="text-2xl font-bold mb-4">Halo, Mahadi 👋</h1>
  <h2 class="text-lg font-semibold">Apa rencanamu hari ini?</h2>

  <PromptForm on:submitted={(e) => {
    dailyPrompt = e.detail;
    localStorage.setItem("dailyPrompt", dailyPrompt);
  }} />

  {#if dailyPrompt}
    <div class="mt-4 p-2 bg-blue-100 rounded">
      <strong>Rencana hari ini:</strong> {dailyPrompt}
    </div>
  {/if}
</main>
