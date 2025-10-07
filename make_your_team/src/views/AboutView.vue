<template>
    <div class="main-container">
        <h1>Sobre o Projeto</h1>
        <p>Este projeto foi desenvolvido como parte de um curso de Vue.js, com o objetivo de criar uma aplicação para montar e gerenciar times de futebol. A aplicação permite adicionar jogadores, visualizar o time atual e obter informações sobre o projeto.</p>
        <h2>Tecnologias Utilizadas</h2>
        <ul>
        <li>Vue.js</li>
        <li>Vue Router</li>
        <li>Fetch API</li>
        <li>CSS para estilização</li>
        </ul>
        <h2>Desenvolvedor</h2>
        <p>Este projeto foi desenvolvido por <b>Vitor Castanheira</b> com o intuito de aprender e praticar Vue.js para evolução na área de desenvolvimento front-end.</p>
    </div>
</template>

<script>
export default {
    name: "AboutView"
}
</script>

<style scoped>
    .main-container {
        max-width: 800px;
        margin: 0 auto;
        padding: 20px;
        font-family: Arial, sans-serif;
        color: #333;
    }

    h1 {
        color: #32c764;
        text-align: center;
        margin-bottom: 20px;
    }

    h2 {
        color: #32c764;
        margin-top: 30px;
    }

    p {
        line-height: 1.6;
        margin-bottom: 15px;
    }

    ul {
        list-style-type: disc;
        padding-left: 20px;
    }

    li {
        margin-bottom: 10px;
    }
</style>