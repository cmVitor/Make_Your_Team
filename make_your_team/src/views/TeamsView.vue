<template>
  <div class="main-container">
    <h1>Gerencie seu time:</h1>
    <Dashboard />
  </div>
</template>

<script>
    import Dashboard from '@/components/Dashboard.vue';

    export default{
      name: "TeamsView",
      components: {
        Dashboard
      }
    }

</script>