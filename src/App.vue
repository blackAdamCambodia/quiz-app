<script setup>
 import {ref, reactive} from 'vue';
 import Questions from "./components/QuestionsView.vue";
 import Result from "./components/ResultView.vue";
 let questionsAnswered = ref(0);
 let totalCorrect= ref(0);
 let questions = reactive([
  {
   q: "what is 2+3?",
   answers: [
      {
        sl: "A.",
        text: " 5",
        isCorrect: true
      },
      {
        sl: "B.",
        text: " 7",
        isCorrect: false
      },
      {
        sl: "C.",
        text: " 9",
        isCorrect: false
      },
      { 
        sl: "D.",
        text: " 11",
        isCorrect: false
      }
   ],
   
  },
  {
   q: "Since Ethereum launched, how many times has the network been offline?",
   answers: [
      {
        sl:"A.",
        text: " Once",
        isCorrect: false
      },
      {
        sl:"B.",
       text: " More then ten times",
        isCorrect: false
      },
      {
        sl:"C.",
        text: " Never",
        isCorrect: true
      },
      {
        sl:"D.",
        text: " Fours times",
        isCorrect: false
      }
   ],
   
  },
  {
   q: "Ethereum’s native cryptocurrency is called:",
   answers: [
      {
        sl:"A.",
        text: "Ether",
        isCorrect: true
      },
      {
        sl:"B.",
       text: " Ethereum",
        isCorrect: false
      },
      {
        sl:"C.",
        text: " Ethercoin",
        isCorrect: false
      },
      {
        sl:"D.",
        text: " Bitcoin",
        isCorrect: false
      }
   ],
   
  },
  
 ]);
let results = reactive ([
  {
    min:0,
    max:2,
    title:"Try Again",
    desc: "Do a little more studying and you may succeed",
  },
  {
    min:3,
    max:3,
    title:"Wow , you are a genius!",
    desc: "Studying has definitely paid off for you!",
  }
])

let questionAnswered = (isCorrect) => {
  
  if(isCorrect){
    totalCorrect.value++;
  }
  questionsAnswered.value++;
}

let reset = () => {
  questionsAnswered.value = 0;
  totalCorrect.value = 0;
}
</script>


<template>
  <div class="ctr">
  <transition name="fade" mode="out-in">
  <Questions 
  v-if="questionsAnswered < questions.length"
  :questions="questions" 
  :questionsAnswered="questionsAnswered"
  @question-answered="questionAnswered"
  /> 
    <Result v-else :results="results" :totalCorrect="totalCorrect"  />
  </transition>
  <button
  type="button"
  @click.prevent="reset"
  class="reset-btn"
  v-if=" questionsAnswered === questions.length"
  >Reset</button>
</div>
</template>

<style scoped>

</style>
