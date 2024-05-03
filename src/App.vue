<template>
    
    <div class="wrapper">
        <h1>{{xWins}} | {{oWins}}</h1>
        <GameBoard :key="componentKey" @haveWinner="(winner) => setScore(winner)" />
        <button class="btn restart" @click="restart">Restart</button>
    </div>
    
</template>

<script>
    import GameBoard from './components/GameBoard.vue';
    
   
    export default {
        name: "App",
        components: { GameBoard },   
        data() {
            return{
                componentKey: 0,
                xWins: 0,
                oWins: 0
            }
        },
        methods: {
            restart(){
                this.componentKey = Math.random()
            },
            setScore(winner){
                winner === "X" ? this.xWins += 1 :this.oWins += 1
            }
        }
    }
</script>

<style lang="scss">


    
</style>