<template>
  <v-app>
    <div class="home">
      <Task1 />
    </div>
  </v-app>
</template>

<script>
// @ is an alias to /src
import Task1 from "@/components/Task1.vue";

export default {
  name: "Home",
  components: {
    Task1,
  },
};
</script>
