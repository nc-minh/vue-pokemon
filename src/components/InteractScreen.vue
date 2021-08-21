<template>
    <div class="wrap">
        <div class="wrap__inner"
            :style="
            {
                width: `${
                    (((VW / (Math.sqrt(cardsContext.length))) - 100) * (Math.sqrt(cardsContext.length)))
                     + 10*(Math.sqrt(cardsContext.length))
                    }px`
            }">
            <Card 
                v-for="(card, index) in cardsContext" 
                :key="index" 
                :imgURL="`img/${card}.png`"   
                :card="{ index, value: card }"
                @onFlip="checkOnFlip"
                :ref="`card-${index}`"
                :cardsContext="cardsContext"
            />
        </div>
    </div>
</template>

<script>
    import Card from "./Card.vue";
    export default {
        props: {
            cardsContext: {
                type: Array,
                default: function () {
                    return [];
                },
            }
        },
        data(){
            return{
                rules: [],
                VW: window.innerWidth
            }
        },
        components: {
            Card,
        },
        methods:{
            checkOnFlip(card){
                console.log(card);
                if(this.rules.length === 2){
                    return false
                }else{
                    this.rules.push(card)
                    console.log('đây là luật: ',this.rules);
                    if(this.rules.length === 2 && this.rules[0].value === this.rules[1].value){
                        console.log('running...');
                        if(this.rules[0].index === this.rules[1].index){
                            this.rules = []
                        }

                        this.$refs[`card-${this.rules[0].index}`].onEnable()
                        this.$refs[`card-${this.rules[1].index}`].onEnable()
                        this.rules = []
                        
                        const point = document.querySelectorAll('.card.disabled')
                        console.log(point)
                        
                        if(point.length === this.cardsContext.length - 2){
                            setTimeout(()=>{
                                this.$emit('onFinish')
                                console.log('emit');
                            }, 1000)
                        }
                    }else if(this.rules.length === 2 && this.rules[0].value !== this.rules[1].value){
                        console.log('wrong...');
                        setTimeout(()=>{
                            this.$refs[`card-${this.rules[0].index}`].onFlipBack()
                            this.$refs[`card-${this.rules[1].index}`].onFlipBack()
                            this.rules = []
                        }, 800)
                    }else{
                        return false
                    }
                }
            }
            
        }
    };
</script>

<style scoped>
.wrap{
    width: 100%;
    height: 100vh;
    top: 0;
    left: 0;
    z-index: 2;
    background-color: var(--dark);
    color: var(--light);
    display: flex;
    justify-content: center;
    align-items: center;
}

.wrap .wrap__inner{
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
}
</style>