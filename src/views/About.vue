<template>
  <v-app>
    <div class="home">
      <Task2 />
    </div>
  </v-app>
</template>

<script>
// @ is an alias to /src
import Task2 from "@/components/Task2.vue";

export default {
  name: "About",
  components: {
    Task2,
  },
};
</script>
