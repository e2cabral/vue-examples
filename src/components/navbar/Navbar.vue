<template>
  <section class="navbar">
    <section class="navbar__link">
      <router-link to="/">Home</router-link>
    </section>
  </section>
</template>

<script>
import { Vue, Component } from 'vue-property-decorator';

@Component
export default class Navbar extends Vue {
}
</script>

<style scoped>

</style>
