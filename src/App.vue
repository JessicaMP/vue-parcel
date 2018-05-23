<template>
  <div>
    <ComponentHeader/>
    <ComponentMain/>
  </div>
</template>

<script>
import ComponentHeader from "./Component-header.vue";
import ComponentMain from "./Component-main.vue";

export default {
  components: {
    ComponentHeader,
    ComponentMain
  }
};
</script>

<style>
body {
  font-family: "Roboto", sans-serif;
}
</style>
