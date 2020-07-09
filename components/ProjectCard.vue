<template>
  <div class="project-card position-relative rounded hover-wrapper" @mouseenter="hover = true" @mouseleave="hover = false">
    <img :src="card.cover" width="100%" height="100%" :alt="card.title" class="img-fluid rounded d-block">
    <div class="hover-overlay">
      <div class="hover-content">
        <div class="h6 text-center project-title">{{card.title}}</div>
        <b-btn class="btn-light" :to="card.path">View Project</b-btn>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
  import Vue from "vue";
  import Component from "nuxt-class-component"
  import {Prop} from "vue-property-decorator";
  import {Project} from "~/models/project";

  @Component
  export default class ProjectCard extends Vue {

    @Prop(Object)
    readonly card: any;

    hover: boolean = false;


  }
</script>

<style scoped>

  .hover-wrapper {
    transition: .3s ease;
    overflow: hidden;
  }

  .hover-wrapper:hover {
    transform: scale(0.9);
  }

  .project-card {
    margin-top: 50px;
  }

  .hover-overlay {
    position: absolute;
    height: 100%;
    width: 100%;
    border-radius: inherit;
    top: 0;
    left: 0;
    background: rgba(0,0,0,.3);
    opacity: 0;
    visibility: hidden;
    transition: .3s ease;
  }

  .hover-wrapper:hover .hover-overlay {
    visibility: visible;
    opacity: 1;
    transition: .3s ease;
  }

  .hover-content {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    left: 0;
    right: 0;
    text-align: center;
  }

  .project-title {
    color: #fff;
    text-shadow: rgba(0, 0, 0, 0.6) 2px 2px 3px;
  }

</style>
