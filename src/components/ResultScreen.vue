<template>
  <div class="screen">
      <h1>Chiến thắng nhé!</h1>
      <p>{{ Math.round(timer / 1000) }}s</p>
      <button @click="onStartAgain">Chơi lại nào^^</button>
  </div>
</template>

<script>
export default {
    props:{
        timer:{
            type: Number,
            required: true
        }
    },
    methods:{
        onStartAgain(){
            this.$emit('onStartAgain')
        }
    }
}
</script>

<style scoped>
.screen{
    height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background-color: rgb(62, 255, 44);
}

.screen h1{
    font-size: 4rem;
    margin-bottom: 30px;
}

.screen p{
    font-size: 2rem;
    color: #2b2b2b;
}

.screen button{
    padding: 10px 20px;
    margin: 0 10px;
    margin-top: 30px;
    border-radius: 10px;
    outline: none;
    background-color: rgb(252, 0, 0);
    cursor: pointer;
    font-size: 1.6rem;
    color: var(--light);
}
</style>