<template>
  <header>
    <h1>{{ title }}</h1>
  </header>
</template>

<script>
export default {
  name: "AppHeader",
  data() {
    return {
      title: "Break it Down, Don't Breakdown",
    };
  },
};
</script>

<style scoped>
header {
  background-color: #4caf50;
  padding: 1rem;
  text-align: center;
  color: white;
}
</style>
