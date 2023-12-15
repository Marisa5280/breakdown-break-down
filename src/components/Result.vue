<template>
  <div>
    <h2>Task: {{ task }}</h2>
    <p>Blockers: {{ blockers }}</p>
    <ul>
      <li v-for="(step, index) in steps" :key="index">
        Step {{ index + 1 }}: {{ step.nextStep }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "TaskStepsResult",
  props: {
    task: String,
    blockers: String,
    steps: Array,
  },
};
</script>