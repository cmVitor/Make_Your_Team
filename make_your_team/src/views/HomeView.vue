<template>
  <div>
    <Banner />
    <div class="main-container">
      <h1>Adicione seu Jogador:</h1>
      <PlayerForm />
    </div>
  </div>

</template>

<script>
import Banner from '@/components/Banner.vue';
import PlayerForm from '@/components/PlayerForm.vue';

export default {
  name: 'HomeView',
  components: {
    Banner,
    PlayerForm
  }
}
</script>
