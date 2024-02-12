<script setup>
import axios from 'axios'
import { ref, onMounted } from 'vue'
import GameOverComponent from '@/components/GameOverComponent.vue';


  let currentQuestion = ref('')
  let correctAnswer = ref('')
  let incorrectAnswer1 = ref('')
  let incorrectAnswer2 = ref('')
  let incorrectAnswer3 = ref('')
  let questionCounter = ref(0)
  let score = ref(0)
  let accessName = localStorage.getItem('name')

  async function getQuestions() {
    axios
      .get('https://the-trivia-api.com/v2/questions?limit=20')
      .then(response => {
        currentQuestion.value = response.data[0]
        correctAnswer.value = currentQuestion.value.correctAnswer
        incorrectAnswer1.value = currentQuestion.value.incorrectAnswers[0]
        incorrectAnswer2.value = currentQuestion.value.incorrectAnswers[1]
        incorrectAnswer3.value = currentQuestion.value.incorrectAnswers[2]
      }

      )

  }

  let allAnswers = ref([correctAnswer, incorrectAnswer1, incorrectAnswer2, incorrectAnswer3])

  function shuffleArray(arr) {
    for (let i = arr.value.length - 1; i > 0; i--) {
        let j = Math.floor(Math.random() * (i + 1)); 
        [arr.value[i], arr.value[j]] = [arr.value[j], arr.value[i]];
    } 
    }

  
  function nextQuestion() {
    if (questionCounter.value <= 20) {
    getQuestions()
    shuffleArray(allAnswers)
    questionCounter.value++
    
   } else {
    console.log('game over!')
   }
  }

  function checkAnswer(answer) {
    if (answer.value === correctAnswer.value) {
      score.value += 10
      nextQuestion()
    } else {
      score.value -= 10
      nextQuestion()
    }
  }

 

  onMounted(() => {
    getQuestions()
    shuffleArray(allAnswers)
  })
  

 
  
</script>

<template>
  <div v-if="questionCounter >= 20" id="game-over">
    <GameOverComponent :yourScore="score" :playerName="accessName"></GameOverComponent>
  </div>
  <div v-else>
    <div id="current-score-container">
      <h3 id="current-score-text">Current Score:</h3>
      <h4 id="current-score"> {{ score }}</h4>
    </div>
    <div id="quiz-container">
      <div id="quiz">
        <div id="question-box" v-for="(question, key) in currentQuestion" :key="key">
          <h3>{{ question.text }}</h3>
        </div>
        <div id="answers" v-for="(answer, key) in allAnswers" :key="key">
          <button @click="checkAnswer(answer)">{{ answer.value }}</button>
        </div>
      </div>
    </div>
  </div>
  
</template>

<style>

  #current-score-container {
    display: flex;
    flex-direction:column;
    text-align: center;
    margin-top: 1rem;
  }

  #current-score-text {
    font-size: 1.4rem;
  }

  #current-score {
    font-size: 1.5rem;
    margin-bottom: 1rem;
    margin-top: 1rem;
  }

  #quiz-container {
    display: flex;
    justify-content: center;
  }

  #quiz {
    background-image: linear-gradient(white, rgb(234, 234, 234));
    height: auto;
    width: 40vw;
    border-radius: 1rem;
    box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.566);
    margin: 1rem;
    padding-bottom: 2rem;
    
  }

  #answers {
    display: flex;
    margin-top: 0.5rem;
    justify-content: center;
  }

  #answers button {
    font-size: 1.5rem;
    font-family: digital;
    width: 20vw;
    border-radius: 0.5rem;
    padding: 0.5rem;
    color: white;
    background-image: linear-gradient(#060561, #383783);
  }

  #answers button:hover {
    background-image: linear-gradient(#282685, #444399);
    cursor: pointer;
  }

  #question-box {
    text-align: center;
    padding-top: 0.5rem;
  }

  #question-box h3 {
    font-size: 1.3rem;
  }

  #game-over {
    display: flex;
    justify-content: center;
    text-align: center;
    margin-top: 3rem;
  }

  @media (min-width: 800px) and (max-width: 1200px) {
    #quiz {
      width: 90vw;
    }

    #answers button {
      width: 50vw;
    }

    footer {
      margin-top: 40rem;
    }
  }

  @media (max-width: 800px) {
    #quiz {
      width: 95vw;
    }

    #answers button {
      width: 80vw;
    }
  }
    

</style>
