<%_ if (rootOptions.router) { _%>
<%# -------------------- IS Using vue-router  -------------------- -%>
<%_   if (!options.isNativeOnly) { _%>
<template web>
  <div class="w-page">
    <nav>
      <ul class="w-navbar">
        <li class="w-title" :text="navbarTitle">{{navbarTitle}}</li>
      </ul>
    </nav>
    <div class="w-container">
      <router-link tag="button" class="w-button" id="homeButton" to="/">Home</router-link>
      <router-link tag="button" class="w-button" id="aboutButton" to="/about">About</router-link>
      <router-view/>
    </div>
  </div>
</template>
<template native>
<%_   } else { _%>
<template>
<%_   } _%>
  <Page>
    <ActionBar :title="navbarTitle"/>
    <GridLayout rows="auto, auto">
      <Button text="Home" @tap="goToHomePage" row="0"/>
      <Button text="About" @tap="goToAboutPage" row="1"/>
    </GridLayout>
  </Page>
</template>
<%_ } else { _%>
<%# -------------------- IS NOT Using vue-router  -------------------- -%>
<%_   if (!options.isNativeOnly) { _%>
<template web>
  <div class="w-page">
    <div class="w-container">
      <img src="~/assets/logo.png" alt="logo" height="20%" width="20%">
      <HelloWorld :msg="msg"/>
    </div>
  </div>
</template>
<template native>
<%_   } else { _%>
<template>
<%_   } _%>
  <Page>
    <ActionBar :title="navbarTitle"/>
    <GridLayout rows="auto, auto">
      <HelloWorld :msg="msg"/>
    </GridLayout>
  </Page>
</template>
<%_ } _%>
<%_ if (!usingTS) { _%>
<%# -------------------- IS NOT Using TypeScript -------------------- -%>
<script>
<%_   if (!rootOptions.router) { _%>
  import HelloWorld from '~/components/HelloWorld';
<%_   } else { _%>
  import Home from '~/views/Home';
  import About from '~/views/About';
<%_   } _%>

<%_   if (!rootOptions.router) { _%>
  const { VUE_APP_MODE, VUE_APP_PLATFORM } = process.env;
<%_   } _%>

  export default {
<%_   if (!rootOptions.router) { _%>
    components: {
      HelloWorld,
    },
<%_     } _%>
    data() {
      return {
        navbarTitle: `App.vue`,
<%_   if (!rootOptions.router) { _%>
        msg: `Mode=${VUE_APP_MODE} and Platform=${VUE_APP_PLATFORM}`,
<%_   } _%>
      };
    },
    methods: {
<%_   if (rootOptions.router) { _%>
      goToHomePage() {
        this.$navigateTo(Home);
      },
      goToAboutPage() {
        this.$navigateTo(About);
      }
<%_   } _%>
    }
  };
</script>
<%_ } else { _%>
<%# -------------------- IS Using TypeScript -------------------- -%>
<script lang="ts">
  import { Component, Vue } from 'vue-property-decorator';
<%_ if (!rootOptions.router) { _%>
  import HelloWorld from '~/components/HelloWorld.vue';
<%_ } else { _%>
  import Home from '~/views/Home.vue';
  import About from '~/views/About.vue';
<%_ } _%>

<%_ if (!rootOptions.router) { _%>
  const { VUE_APP_MODE, VUE_APP_PLATFORM } = process.env;
<%_ } _%>

  @Component({
    name: 'home',
<%_ if (!rootOptions.router) { _%>
    components: {
      HelloWorld,
    },
<%_ } _%>
  })
  export default class App extends Vue {
    private navbarTitle: string = `App.vue`;
<%_ if (!rootOptions.router) { _%>
    private msg: string = `Mode=${VUE_APP_MODE} and Platform=${VUE_APP_PLATFORM}`;
<%_ } _%>

<%_ if (rootOptions.router) { _%>
    public goToHomePage() {
      Vue.prototype.$navigateTo(Home);
    }

    public goToAboutPage() {
      Vue.prototype.$navigateTo(About);
    }
<%_ } _%>
  }

</script>
<%_ } _%>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<%_ if (rootOptions.cssPreprocessor) { _%>
<%_   if (rootOptions.cssPreprocessor == 'sass' || rootOptions.cssPreprocessor == 'scss') { _%>
<%#   -------------------- IS Using scss OR sass -------------------- -%>
<%- rootOptions.cssPreprocessor
    ? `<style web lang="${
        rootOptions.cssPreprocessor === 'sass'
          ? 'scss'
          : rootOptions.cssPreprocessor
      }"` + `>`
    : ``
%>
  @import '~styles/style-one';

  .w-page {
    height: 100%;
    width: 100%;
  }

</style>
<%- rootOptions.cssPreprocessor
    ? `<style native lang="${
        rootOptions.cssPreprocessor === 'sass'
          ? 'scss'
          : rootOptions.cssPreprocessor
      }"` + `>`
    : ``
%>
  @import '~styles/style-one';
</style>
<%_   } else if (rootOptions.cssPreprocessor == 'stylus') { _%>
<%#   -------------------- IS Using stylus -------------------- -%>
<style web lang="stylus">
  @import '~styles/style-one';

  .w-page
    height 100%
    width 100%

</style>
<style native lang="stylus">
  @import '~styles/style-one';
</style>
<%_   } else if (rootOptions.cssPreprocessor == 'less') { _%>
<%#   -------------------- IS Using Less -------------------- -%>
<style web lang="less">
  @import '~styles/style-one';

  .w-page {
    height: 100%;
    width: 100%;
  }

</style>
<style native lang="less">
  @import '~styles/style-one';
</style>
<%_   } _%>
<%_ } else { _%>
<%# -------------------- IS Using standard CSS -------------------- -%>
<style web lang="scss">
  @import '~styles/style-one';

  .w-page {
    height: 100%;
    width: 100%;
  }
</style>
<style native lang="scss">
  @import '~styles/style-one';
</style>
<%_ } _%>