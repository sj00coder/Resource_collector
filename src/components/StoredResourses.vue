<template>
  <ul>
    <learning-component
      v-for="resource in resources"
      :resource="resource"
      :key="resource.id"
      :id="resource.id"
    ></learning-component>
  </ul>
</template>

<script>
import LearningComponent from "./LearningComponent";
export default {
  inject: ["resources"],
  components: {
    LearningComponent,
  },
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>