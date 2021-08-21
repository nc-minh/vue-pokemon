<template>
  <div class="card"
    :class="{ disabled: isDisabled }"
    :style="
    { 
        height: `${(VH / (Math.sqrt(cardsContext.length))) - 10 }px`,
        width: `${(VW / (Math.sqrt(cardsContext.length))) - 100}px` 
    }">
      <div class="card__inner" 
        :class="{ 'is-flipped': isFlipped }"
        @click="onToggleFlipCard"
        >
          <div class="card__face card__face--front">
              <div class="card__content"></div>
          </div>
          <div class="card__face card__face--back">
              <div class="card__content"
                :style="{ backgroundImage: `url(${require('@/assets/' + imgURL)})` }"
              ></div>
          </div>
      </div>
  </div>
</template>

<script>
export default {
    data() {
        return {
            isFlipped: false,
            isDisabled: false,
            VH: window.innerHeight,
            VW: window.innerWidth
        }
    },
    props:{
        imgURL:{
            type: String,
            required: true
        },
        card:{
            type: [Number, Array, String, Object]
        },
        cardsContext: {
            type: Array,
            default: function () {
                return [];
            },
        }
    },
    methods: {
        onToggleFlipCard(){
            if(this.isDisabled){
                return false
            }
            this.isFlipped = !this.isFlipped
            if(this.isFlipped){
                this.$emit('onFlip', this.card)
            }
            
        },
        onFlipBack(){
            this.isFlipped = false
        },
        onEnable(){
            this.isDisabled = true
        }
    },
}
</script>

<style scoped>
.card{
    display: flex;
    margin: 0.5rem;
}

.card__inner{
    width: 100%;
    height: 100%;
    transition: transform 1s;
    transform-style: preserve-3d;
    cursor: pointer;
    position: relative;
}

.card__inner.is-flipped{
    transform: rotateY(-180deg);
}

.card__face{
    position: absolute;
    width: 100%;
    height: 100%;
    backface-visibility: hidden;
    overflow: hidden;
    border-radius: 1rem;
    padding: 1rem;
    box-shadow: 0 3px 10px 3px rgba(0, 0, 0, 0.2);
}

.card__face--back{
    background-color: var(--light);
    transform: rotateY(-180deg);
}

.card__face--front .card__content{
    background: url('../assets/img/icon_back.png') no-repeat center center;
    background-size: contain;
    width: 100%;
    height: 100%;
}

.card__face--back .card__content{
    background-size: contain;
    background-repeat: no-repeat;
    background-position: center center;
    height: 100%;
    width: 100%;
}

.card.disabled .card__inner{
    cursor: default;
}
</style>