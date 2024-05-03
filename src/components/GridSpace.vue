<template>
    <div class="space"  @click.prevent.left="clickSpace" @mousemove="makeRainbow">
        <h1>{{spaceTurn}}</h1>
    </div>
</template>

<script>
//:class="{rainbow: spaceTurn === winner}"
export default {
    name: "GridSpace",
    props: ['spaceContent', 'handleClick', 'index', 'winner'],
    data(){
        return {
            spaceTurn: ""
        }
    },
    methods: {
        clickSpace() {
            if(this.winner === undefined){
                this.spaceTurn = this.spaceContent;     
                this.$emit('clickedSpace')
            }
        },
        makeRainbow() {
            if(this.winner !== undefined){

            }
        }
    }
}
</script>
