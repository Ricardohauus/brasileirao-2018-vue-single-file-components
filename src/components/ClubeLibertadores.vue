<template>
  <div>
    <h3>Times Classificados para Libertadores</h3>
    <ul>
      <li v-for="time in timesLibertadores">
        <clube :time="time"></clube>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ["times"],
  computed: {
    timesLibertadores() {
      return this.times.slice(0, 6);
    }
  }
};
</script>