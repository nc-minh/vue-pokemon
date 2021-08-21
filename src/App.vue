<template> 
  <MainScreen 
    v-if="statusMatch === 'default'"
    @onStart="onStart($event)"
    />
  <InteractScreen 
    v-if="statusMatch === 'match'"
    :cardsContext="settings.cardsContext"
    @onFinish="getResult"
  />
  <ResultScreen
    v-if="statusMatch === 'result'"
    :timer="timer"
    @onStartAgain="statusMatch = 'default'"
  />
</template>

<script>
import MainScreen from './components/MainScreen.vue'
import InteractScreen from './components/InteractScreen.vue'
import ResultScreen from './components/ResultScreen.vue'
import {shuffled} from './utils/array'
export default {
  name: 'App',
  data() {
    return {
      statusMatch: 'default',
      settings:{
        totalOfBlock: 0,
        cardsContext: [],
        startedAt: null
      },
      timer: 0,
    }
  },
  methods:{
    onStart(config){
      console.log('running....',config)
      this.settings.totalOfBlock = config.totalOfBlock
      const firstCard = Array.from( { length: this.settings.totalOfBlock / 2 }, (_, i)=>i+1 )
      console.log(firstCard);

      const secondCard = [...firstCard]
      console.log(secondCard);

      const cards = [...firstCard, ...secondCard]
      console.log(cards);

      this.settings.cardsContext = shuffled(shuffled(shuffled(shuffled(cards))))

      console.log(this.settings.cardsContext);

      this.settings.startedAt = new Date().getTime();
      console.log(this.settings.startedAt);

      this.statusMatch = 'match'
    },
    getResult(){
      //get time
      //switch resultScreen
      this.statusMatch = 'result'
      this.timer = new Date().getTime() - this.settings.startedAt
    }
  },
  components: {
    MainScreen,
    InteractScreen,
    ResultScreen
  }
}
</script>

<style>

</style>
