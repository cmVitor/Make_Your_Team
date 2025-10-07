<template>
    <Message :msg="msg" v-show="msg" />
    <div>
        <form id="player-form" method="POST" @submit="createPlayer">
            <div class="input-container">
                <label for="nome">Nome do Jogador:</label>
                <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite o nome">
            </div>
            <div class="input-container">
                <label for="posicao">Selecione a posição:</label>
                <select name="posicao" id="posicao" v-model="posicao">
                    <option value="">Selecione</option>
                    <option v-for="posicao in posicoes" :key="posicao.id" :value="posicao.tipo">
                        {{ posicao.tipo }}</option>
                </select>
            </div>
            <div class="input-container">
                <label for="perna">Selecione a perna boa:</label>
                <select name="perna" id="perna" v-model="perna">
                    <option value="">Selecione</option>
                    <option v-for="perna in pernas" :key="perna.id" :value="perna.tipo">
                        {{ perna.tipo }}</option>
                </select>
            </div>
            <div id="diferenciais-container" class="input-container">
                <label id="diferenciais-title" for="diferenciais">Selecione os diferenciais:</label>
                <div class="checkbox-container" v-for="diferencial in diferenciaisdata" :key="diferencial.id">
                    <input type="checkbox" name="diferenciais" v-model="diferenciais" :value="diferencial.tipo">
                    <span>{{ diferencial.tipo }}</span>
                </div>
            </div>
            <div class="input-container">
                <input class="submit-btn" type="submit" value="Adicionar Jogador!">
            </div>

        </form>
    </div>
</template>

<script>
import Message from './Message.vue';
export default {
    name: "PlayerForm",
    data() {
        return {
            posicoes: null,
            pernas: null,
            diferenciaisdata: null,
            nome: null,
            posicao: null,
            perna: null,
            diferenciais: [],
            status: "Titular",
            msg: null
        }
    },
    methods: {
        async getCaracteristicas() {
            const req = await fetch('http://localhost:3000/caracteristicas');
            const data = await req.json()

            this.posicoes = data.posicoes;
            this.pernas = data.pernas;
            this.diferenciaisdata = data.diferenciais
        },
        async createPlayer(e) {
            
            e.preventDefault();

            const data = {
                nome: this.nome,
                perna: this.perna,
                posicao: this.posicao,
                diferenciais: Array.from(this.diferenciais),
                status: "Titular"
            }

            const dataJson = JSON.stringify(data);

            const req = await fetch('http://localhost:3000/players', {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: dataJson
            });

            const res = await req.json()

            console.log(res)

            this.msg = "Jogador cadastrado com sucesso!"

            // clear message
            setTimeout(() => this.msg = "", 3000)


            // limpar campos
            this.nome = ""
            this.posicao = ""
            this.perna = ""
            this.diferenciais = []
        }
    },
    mounted() {
        this.getCaracteristicas()
    },
    components: {
        Message
    }
}
</script>

<style scoped>
#player-form {
    max-width: 400px;
    margin: 0 auto;
}

.input-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
}

label {
    font-weight: bold;
    margin-bottom: 15px;
    color: #222;
    ;
    padding: 5px 10px;
    border-left: 4px solid #32c764;
}

input,
select {
    padding: 5px 10px;
    width: 300px;
}

#diferenciais-container {
    flex-direction: row;
    flex-wrap: wrap;
}

#diferenciais-title {
    width: 100%;
}

.checkbox-container {
    display: flex;
    align-items: flex-start;
    width: 50%;
    margin-bottom: 20px;
}

.checkbox-container span,
.checkbox-container input {
    width: auto;
}

.checkbox-container span {
    margin-left: 6px;
    font-weight: bold;
}

.submit-btn {
    background-color: #222;
    color: #32c764;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
    border-radius: 25px;
}

.submit-btn:hover {
    background-color: transparent;
    color: #222;
}
</style>