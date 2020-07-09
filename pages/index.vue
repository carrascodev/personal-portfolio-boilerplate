<template>
  <section id="intro">
    <Banner/>
    <div class="container">
      <b-row class="justify-content-center">
        <b-col md="1"></b-col>
        <b-col md="10">
          <b-card class="card-profile shadow border-0">
            <b-card-body class="text-center">
              <b-card-img :src="intro.authorImg" class="rounded-circle profile-image"></b-card-img>
              <b-card-title>{{intro.name}}</b-card-title>
              <div class="h6 font-weight-light">{{intro.role}}<span v-if="intro.company.include"> @ <a :href="intro.company.site" target="_blank">{{intro.company.name}}</a></span></div>
              <hr>
              <p class="m-5">{{intro.description}} <a :href="intro.resume">{{$t('intro.resume')}}</a></p>
              <a :href="'http://linkedin.com/in/'+intro.linkedin" target="_blank">
                <font-awesome-icon :icon="['fab', 'linkedin']" style="font-size: 30px"/>
              </a>
              <a :href="'http://twitter.com/'+intro.twitter" target="_blank">
                <font-awesome-icon :icon="['fab', 'twitter-square']" style="font-size: 30px"/>
              </a>
              <a href="#"
                 @click="copyToClipboard(intro.discord)"
                 v-b-tooltip.hover :title="intro.discord"
              >
                <font-awesome-icon :icon="['fab', 'discord']" style="font-size: 30px"/>
              </a>
              <a :href="intro.whatsapp" target="_blank">
                <font-awesome-icon :icon="['fab', 'whatsapp-square']" style="font-size: 30px"/>
              </a>
            </b-card-body>
          </b-card>
        </b-col>
        <b-col md="1"></b-col>
      </b-row>

    </div>
  </section>
</template>

<script lang="ts">
  import Vue from 'vue'
  import Component from 'nuxt-class-component';
  import { ToastPlugin } from 'bootstrap-vue'

  @Component
  export default class Home extends Vue {

    async asyncData(context: any) {
      console.log("asyncData set")
      return {
        intro: await context.$content('intro').fetch()
      }
    }

    copyToClipboard(text: string) {
      var dummy = document.createElement("textarea");
      document.body.appendChild(dummy);
      dummy.value = text;
      dummy.select();
      document.execCommand("copy");
      document.body.removeChild(dummy);
      this.onCopied();
    }

    onCopied() {
      this.$bvToast.toast('Discord id copied', {
        title: "Notification",
        variant: 'success',
        solid: true,
        autoHideDelay: 5000,
      });
    }
  }

  Vue.use(ToastPlugin)
</script>

<style scoped>

  .card-profile {
    margin-top: -50px;
    color: #37383b;
    font-family: "Droid Sans";
  }

  .card-profile .profile-image {
    width: 200px;
    height: 200px;
    margin-top: -100px;

  }
  .card-title {
    margin-top: 50px;
  }



</style>
