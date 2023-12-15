<template>
  <div>
    <AppHeader />
    <template v-if="currentForm === 'taskForm'">
      <InputForm
        :formFields="taskFormFields"
        submitButtonText="Break it Down"
        @submit="handleBreakDown"
      />
    </template>
    <template v-else-if="currentForm === 'stepForm'">
      <InputForm
        :formFields="stepFormFields"
        submitButtonText="Next Step"
        @submit="handleNextStep"
      />
      <button @click="handleDone">Done</button>
    </template>
    <template v-else>
      {{ currentForm }}
      <TaskStepsResult :task="task" :blockers="blockers" :steps="steps" />
    </template>
  </div>
</template>

<script>
import AppHeader from "@/components/Header.vue";
import InputForm from "@/components/InputForm.vue";
import TaskStepsResult from "@/components/Result.vue";

export default {
  name: "LandingPage",
  components: {
    AppHeader,
    InputForm,
    TaskStepsResult,
  },
  data() {
    return {
      currentForm: "taskForm",
      taskFormFields: [
        {
          id: "bigPictureTask",
          label: "What is the big picture task?",
          type: "text",
          placeholder: "Enter the task",
          value: "",
        },
      ],
      stepFormFields: [
        {
          id: "blockers",
          label: "Any blockers?",
          type: "text",
          placeholder: "Enter blockers",
          value: "",
        },
        {
          id: "nextStep",
          label: "Next Step",
          type: "text",
          placeholder: "Enter the next step",
          value: "",
        },
      ],
      task: "",
      blockers: "",
      steps: [],
    };
  },
  methods: {
    handleBreakDown(formData) {
      this.task = formData.bigPictureTask;
      this.currentForm = "stepForm";
    },
    handleNextStep(formData) {
      console.log("formData:", formData);
      const newStep = { nextStep: formData.nextStep };
      console.log("new step", newStep);
      this.steps.push(newStep);
      console.log("updated steps", this.steps);

      // Clear the value of nextStep in the form after pushing to steps
      this.stepFormFields.find((field) => field.id === "nextStep").value = "";

      console.log("form fields after clearing nextStep:", this.stepFormFields);
    },
    handleDone() {
      console.log("Final State:", {
        task: this.task,
        blockers: this.blockers,
        steps: this.steps,
      });
      this.currentForm = "resultForm";
    },
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
