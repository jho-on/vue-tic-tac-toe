<template>
    <button class="btn changeMarkers">Change X/O</button>
    <div v-if="winner != undefined" class="winMsg">
        <h1>{{winner}} wins</h1>
    </div>
    
    <div class="gameBoard">
        <GridSpace v-for="(space, index) in gameState"
        :key="index" :index="index" 
        :spaceContent="turn" 
        @clickedSpace="() => switchTurn(index)" :winner="winner">

        </GridSpace>
    </div>

    
</template>

<script>
    import GridSpace from './GridSpace.vue';

    export default {
        name: "GameBoard",
        components: { GridSpace },
        emits: ['haveWinner'],
        data() {
            return {
                gameState: 
                [
                    [''], [''], [''],
                    [''], [''], [''],
                    [''], [''], ['']
                ],
                turn: "X",
                winner: undefined
            }
        },
        methods: {
            testEnd() {
                let makeRainbowIndex = undefined;
                for(let i = 0; i <= 2; i++){
                    if(this.gameState[i] == this.gameState[i + 3] && this.gameState[i + 3] == this.gameState[i + 6]){
                        makeRainbowIndex = [i, i + 3, i + 6]
                    }
                }
                for(let i = 0; i <= 6; i += 3){
                    if(this.gameState[i] == this.gameState[i + 1] && this.gameState[i + 1] == this.gameState[i + 2]){
                        makeRainbowIndex = [i, i + 1, i + 2]
                    }
                }
                if(this.gameState[0] == this.gameState[4] && this.gameState[4] == this.gameState[8]){
                    makeRainbowIndex = [0, 4, 8]
                }
                if(this.gameState[2] == this.gameState[4] && this.gameState[4] == this.gameState[6]){
                    makeRainbowIndex = [2, 4, 6]
                }

                if(makeRainbowIndex !== undefined){
                    makeRainbowIndex.forEach((element) => (document.getElementsByClassName("gameBoard")[0].children[element].className = "space rainbow"))
                    return true
                }
                

                return false
            },
            switchTurn(index) {
                this.gameState[index] = this.turn;
                if(this.testEnd()){
                    this.winner = this.turn;
                    this.$emit("haveWinner", String(this.winner));
                    
                }
                return this.turn === "X" ? this.turn = "O" : this.turn = "X";
            }

        }
    }

</script>
