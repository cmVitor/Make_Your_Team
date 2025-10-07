<template>
    <div id="main-banner">
        <h1>Monte seu time</h1>
    </div>
</template>

<script>
    export default{
        name: "Banner"
    }
</script>

<style scoped>
 #main-banner {
    background-image: url('/public/img/soccer.jpg');
    background-position: 0 -250px;
    background-size: cover;
    height: 350px;
    display: flex;
    align-items: center;
    justify-content: flex-start;
  }

  #main-banner h1 {
    color: #FFF;
    text-align: center;
    font-size: 60px;
    background-color: #222;
    padding: 20px 40px;
  }

</style>
