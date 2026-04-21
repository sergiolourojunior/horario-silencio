<template>
  <div class="min-h-screen flex justify-center items-center" :class="can ? 'bg-green-300 text-green-900' : 'bg-red-300 text-red-900'">
    <div>
      <h1 class="text-xl font-medium mb-4">Pode fazer barulho?</h1>
      <div class="text-5xl font-bold text-center">
        <div v-if="can">Sim 👍</div>
        <div v-else>Não 👎</div>
      </div>
    </div>
    <div class="fixed bottom-3 text-sm">
      <strong class="font-semibold">Os horários permitidos são:</strong>
      <ul class="font-light">
        <li>Segunda à sexta das 8h às 12h e das 14h às 18h</li>
        <li>Sábado das 8h às 12h</li>
        <li>Domingo e Feriados não pode fazer barulho</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  computed: {
    can() {
      const now = new Date();
      const weekday = now.getDay();
      const hours = now.getHours();
      const minutes = now.getMinutes();

      if (weekday >= 1 && weekday <= 5) {
        return ((hours > 8 || (hours === 8 && minutes >= 0)) && (hours < 12 || (hours === 12 && minutes === 0)) || (hours > 14 || (hours === 14 && minutes >= 0)) && (hours < 18 || (hours === 18 && minutes === 0)));
      }

      if (weekday === 6) {
        return (hours > 8 || (hours === 8 && minutes >= 0)) && (hours < 12 || (hours === 12 && minutes === 0));
      }

      return false;

    }
  }
}
</script>

<style src="./assets/style/app.css" />
