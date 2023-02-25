<template>
    <div style="padding: 20px;">
      <principal/>
    </div>
  </template>
  
  <script>
  import principal from '../../components/dashboard/principal.vue';
  export default {
    auth: true,
    layout: 'dashboard',
    components: {
      principal
    }
  }
  </script>