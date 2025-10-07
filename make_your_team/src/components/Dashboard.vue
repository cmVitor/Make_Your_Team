<template>
    <div id="player-table" v-if="players">
        <div>
            <div id="player-table-heading">
                <div class="player-id">#:</div>
                <div>Jogador:</div>
                <div>Posição:</div>
                <div>Perna Boa:</div>
                <div>Diferenciais:</div>
                <div>Ações:</div>
            </div>
        </div>

        <div id="player-table-rows">
            <div class="player-table-row" v-for="player in players" :key="player.id">
                <div class="player-number">{{ player.id }}</div>
                <div>{{ player.nome }}</div>
                <div>{{ player.posicao }}</div>
                <div>{{ player.perna }}</div>
                <div>
                    <ul>
                        <li v-for="(diferencial, index) in player.diferenciais" :key="index">
                            {{ diferencial }}
                        </li>
                    </ul>
                </div>
                <div class="acoes">
                    <select name="status" class="status" @change="updatePlayer($event, player.id)">
                        <option value="">Status</option>
                        <option v-for="s in status" :key="s.id" :value="s.tipo" :selected="player.status == s.tipo">
                            {{ s.tipo }}
                        </option>
                    </select>
                    <button class="delete-btn" @click="deletePlayer(player.id)">Excluir</button>
                </div>
            </div>
        </div>

    </div>


</template>

<script>
export default {
    name: "Dashboard",
    data() {
        return {
            players: null,
            player_id: null,
            status: []
        }
    },
    methods: {
        async getPlayers() {
            const req = await fetch('http://localhost:3000/players')

            const data = await req.json()

            this.players = data

            this.getStatus()
        },
        async getStatus() {
            const req = await fetch('http://localhost:3000/status')

            const data = await req.json()

            this.status = data;

        },
        async deletePlayer(id) {
            const req = await fetch(`http://localhost:3000/players/${id}`, {
                method: "DELETE"
            });

            const res = await req.json()

            this.getPlayers()
        },
        async updatePlayer(event, id) {
            const option = event.target.value;

            const dataJson = JSON.stringify({ status: option });

            const req = await fetch(`http://localhost:3000/players/${id}`, {
                method: "PATCH",
                headers: { "Content-Type": "application/json" },
                body: dataJson
            });

            const res = await req.json()

            console.log(res)
        }
    },
    mounted() {
        this.getPlayers()
    }
}

</script>

<style scoped>
  #player-table {
    max-width: 1200px;
    margin: 0 auto;
  }

  #player-table-heading,
  #player-table-rows,
  .player-table-row {
    display: flex;
    flex-wrap: wrap;
  }

  #player-table-heading {
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333;
  }

  .player-table-row {
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid #CCC;
  }

  #player-table-heading div,
  .player-table-row div {
    width: 19%;
  }

  #player-table-heading .player-id,
  .player-table-row .player-number {
    width: 5%;
  }

  select {
    padding: 12px 6px;
    margin-right: 12px;
  }

  .delete-btn {
    background-color: #222;
    color:#ff0000;
    font-weight: bold;
    border: 2px solid #222;
    border-radius: 15px;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
    max-height: 40px;
  }
  
  .delete-btn:hover {
    background-color: transparent;
    color: #222;
  }
  .status{
    border-radius: 25px;
    background-color: #e3ffec;
    text-align: center;
    max-height: 40px;
  }
  .acoes{
    display: flex;
    align-items: center;
  }
  
</style>