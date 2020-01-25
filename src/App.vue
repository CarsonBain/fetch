<template>
  <div id="app" class="h-full font-body bg-gray-100 text-gray-900">
    <Nav title="Fetch"></Nav>
    <Dogs />
  </div>
</template>

<script>
import Dogs from "./components/Dogs.vue";
import Nav from "./components/Nav.vue";

export default {
  name: "app",
  components: {
    Dogs,
    Nav
  }
};
</script>

<style src="./assets/css/tailwind.css">
