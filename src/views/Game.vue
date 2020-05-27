<template>
  <div class="game">
        <header>
                <center><u><h1>Guess-O-Mania</h1></u></center>
                <a href="/">Game</a>
                <a href="/scoreboard">Scoreboard</a>
                <a href="/help">Help</a>
        </header>
        <u><h3 id="guess">Make your guess:</h3></u>
        
        <form ref="sheet" method="POST" action="https://www.w3schools.com/tags/att_form_action.asp" >
            <input class="tb" type="text" name="name" placeholder="Enter Your Name" style="width:265px;" required><br><br>
            <input type="text" name="score" id="display" v-model="score" disabled>&emsp;&emsp;
            <input type="hidden" name="score" id="final" v-model="score">
            <input type="button" value="Finish the Game" id="sng" @click="savescore()" style="width:265px;" ><br><br>
        </form>
        <form id="arena" >
            <span v-for="(button,i) in buttons" :key="i">
                <input type="button" :value="button.name" :style="button.style" @click="handler(i+1)">
            </span>
        </form>
        <footer>
            <p><b>Guess-O-Mania</b></p>
        </footer>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from "axios";
export default {
  name: "Game",
  data(){
           return{
                title:'Guess-O-Mania',
                score:0,
                buttons:[],
                list:["","AliceBlue","AntiqueWhite","Aqua","Azure","Beige"]}
        },created(){
            this.fetchbuttons()
        },
        methods:{
            handler:function(index){
                var t=0
                if(index==5){
                    t=100
                }else if(index==4){
                    t=80
                }else if(index==3){
                    t=60
                }else if(index==2){
                    t=40
                }else{
                    t=70
                }
                var c=Math.floor(Math.random() * 5)+1
                console.log(c)
                if (this.list[index]===this.list[c]){
                    this.score+=t
                }else{
                    this.score-=20
                    
                    this.score=(this.score>0)?this.score:0
                }
            },
            fetchbuttons:async function(){
                let temp=await axios.get("http://localhost:3000/buttons")
                this.buttons=temp.data
            },
            savescore:function(){
                if(confirm('Your Final Score is '+this.score)){
                    this.$nextTick(() => {
                        this.$refs.sheet.submit();
                      });
                }
            }
            
        }
};
</script>
<style scoped>
.game{
    columns: #333333;
    font-family: Arial, Helvetica, sans-serif;
    min-height: 100vh;
    margin: 0 auto;
    padding: 0 16px;
    display: flex;
    flex-direction: column;
}

.game{
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
input{
    border:1px solid #cccccc;
    padding:8px;
}
.tb{
    cursor:auto;
}
.tb:hover{
    background-color: whitesmoke;
}
.scoreboard,th,td{
    padding:5px;
    border-collapse: collapse;
    border: 2px solid black;
    text-align: center;
}
input,button{
    cursor: pointer;
    padding: 15px 25px;
    font-size: 24px;
    text-align: center;
    width:155px;
    max-width: 265px;
    cursor: pointer;
    outline: none;
    border-radius: 15px;
    border:1px solid #888888;
    padding:8px;
    box-shadow: 0 9px #999;
    margin: 10px 10px;
  }
  
input:hover {background-color: #3e8e41}
  
input:active ,button:active{
    box-shadow: 0 5px #666;
    transform: translateY(4px);
}

#display {
    width: 265px;
    max-width: 270px;
    font-size: 26px;
    text-align: right;
    background-color: #bcbd95;
    float: left;
}



</style>