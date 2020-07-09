<template>
  <div>
    <footer class="text-center text-black-50">
        Copyright© 2020
    </footer>
  </div>
</template>

<script lang="ts">
  import Vue from "vue";
  import Component from "nuxt-class-component";

  @Component
  export default class Footer extends Vue {

  }
</script>

<style scoped>
footer {
  margin-top: 50px;
}
</style>
