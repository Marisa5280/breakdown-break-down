<template>
  <div>
    <div v-for="(field, index) in formFields" :key="index">
      <label>{{ field.label }}</label>
      <input
        v-if="field.type === 'text'"
        type="text"
        v-model="field.value"
        :placeholder="field.placeholder"
      />
      <!-- Add other form element types as needed -->
    </div>
    <button @click="submitForm">{{ submitButtonText }}</button>
  </div>
</template>

<script>
export default {
  props: {
    formFields: Array,
    submitButtonText: String,
  },
  methods: {
    submitForm() {
      // Handle form submission, you can emit an event or call a parent method
      // to handle the form data.
      this.$emit('submit', this.formFields);
    },
  },
};
</script>

<style scoped>
form {
  margin: 1rem;
}

label {
  margin-right: 1rem;
}
</style>
