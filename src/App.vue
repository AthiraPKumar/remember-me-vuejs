<!-- this is the root component -->
<template>
  <the-header title="Remember Me"></the-header>
  <the-resources></the-resources>
</template>

<script>

import TheHeader from './components/layouts/TheHeader.vue';
import TheResources from './components/Learning-Resource/TheResources.vue';

export default {
  components: {
    TheHeader,
    TheResources
  }
};
</script>

<style>
@import url("http://fonts.googleapis.com/css?family=Roboto");

* {
  box-sizing: border-box;
}
html {
 font-family: 'Roboto', sans-serif;
}
body {
  margin: 0;
}

</style>
