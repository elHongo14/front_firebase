<template>
  <login />
</template>

<script>
import login from '../components/user/login.vue'
export default {
  name: 'IndexPage',
  layout: 'login',
  components: {
    login
  }
}
</script>

<style scoped>
</style>
