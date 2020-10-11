<template>
  <div id="app">
    <Multiselect :list="list" />
  </div>
</template>

<script>
import Multiselect from "@/components/Multiselect";

export default {
  name: "App",
  data() {
    return {
      list: ["USA", "Germany", "France", "Poland", "Russia", "Japan"],
    };
  },
  components: {
    Multiselect,
  },
};
</script>
