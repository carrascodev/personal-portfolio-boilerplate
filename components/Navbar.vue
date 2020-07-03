<template>
  <div>
    <!-- As a link -->
    <BNavbar toggleable="sm" variant="faded" type="light">
      <BNavbarToggle target="nav-collapse"></BNavbarToggle>
      <BNavbarBrand>Portfolio</BNavbarBrand>
      <BCollapse id="nav-collapse" is-nav>
        <BNavbarNav align="right">
          <BNavItem to="/">Home</BNavItem>
          <BNavItem to="/about">About</BNavItem>
          <BNavItem to="/work">Work</BNavItem>
          <BNavItem to="/articles">Articles</BNavItem>
          <BNavItem to="/contact">Contact</BNavItem>
        </BNavbarNav>
      </BCollapse>

    </BNavbar>
  </div>
</template>

<script lang="ts">
  import Vue from "vue";
  import Component from "nuxt-class-component";

    @Component
    export default class Navbar extends Vue {

    }
</script>

<style scoped>

</style>
