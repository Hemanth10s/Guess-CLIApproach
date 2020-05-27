<template>
  <div class="score">
    <header>
            <center><u><h1>Guess-O-Mania</h1></u></center>
            <a href="/">Game</a>
            <a href="/scoreboard">Scoreboard</a>
            <a href="/help">Help</a>
        </header>
            <h3><u>Top 5:</u></h3>
            <table class="scoreboard">
                <tr>
                    <th>Name</th>
                    <th>Score</th>
                </tr>
                <tr v-for="score in scores" :key="score.id">
                    <td>{{score.name}}</td>
                    <td>{{score.score}}</td>
                </tr>
        </table>
  </div>
</template>
<script>
import axios from "axios"
export default {
  name:'Scoreboard',
  data(){
        return {scores:{}}
    },
    created(){
        this.fetchscores()
    },
    methods:{
        fetchscores:async function(){
            let temp=await axios.get("https://fathomless-cliffs-77664.herokuapp.com/get-scores")
            this.scores=temp.data.slice(0,5)
        }
    }
}
</script>

<style scoped>
.score{
    columns: #333333;
    font-family: Arial, Helvetica, sans-serif;
    min-height: 100vh;
    margin: 0 auto;
    padding: 0 16px;
    display: flex;
    flex-direction: column;
}

.score{
    flex-grow: 1;
}

footer{
    color:#888888;
    border-top:1px solid #eeeeee;
    margin-top: 16px;
    padding: 16px 0;
}

header{
    margin-top: 16px;
    margin-bottom: 48px;
}

h1{
    font-size: 64px;
    margin-bottom: 16px;
}

header a{
    color: #888888;
    margin-right: 16px;
    text-decoration: none;
}

.portrait{
    width: 256px;
}


.scoreboard,th,td{
    padding:5px;
    border-collapse: collapse;
    border: 2px solid black;
    text-align: center;
}




</style>
