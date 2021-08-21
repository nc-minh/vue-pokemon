<template>
  <div class="screen">
      <h1>Pokémon Game</h1>
      <h3>Select mode  to start game!</h3>
      <div class="actions">
          <button @click="onStart(16)">
              <span>4x4 - Easy</span>
          </button>
          <button @click="onStart(36)">
              <span>6x6 - Normal</span>
          </button>
          <button @click="onStart(64)">
              <span>8x8 - Hard</span>
          </button>
          <button @click="onStart(100)">
              <span>10x10 - Master</span>
          </button>
      </div>
  </div>
</template>

<script>
export default {
    methods:{
        onStart(totalOfBlock){
            this.$emit('onStart', { totalOfBlock })
        }
    }
}
</script>

<style scoped>
.screen{
    width: 100%;
    height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background-color: rgb(255, 208, 108);
    background-image: url('../assets/img/bg.jpg');
    background-size: cover;
    background-position: bottom left;
}

.screen h1{
    font-size: 4rem;
    margin-bottom: 30px;
}

.screen h3{
    font-size: 2rem;
    color: #2b2b2b;
}

.actions{
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
}

.actions button{
    padding: 10px 20px;
    margin: 0 10px;
    margin-top: 30px;
    border-radius: 10px;
    outline: none;
    background-color: lawngreen;
    cursor: pointer;
    font-size: 1.6rem;
}
</style>