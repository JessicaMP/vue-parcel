<template>
  <div>
    <ComponentHeader/>
    <ComponentMain/>
  </div>
</template>

<script>
import ComponentHeader from "./components/Component-header";
import ComponentMain from "./components/Component-main";

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
