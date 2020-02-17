<template>
  <div class="questions-wrapper">
    <span v-if="isRequesting"> Loading... </span>
      <template v-if="currentQuestion && !isRequesting">
        <h2>
          {{currentQuestion.question}}
        </h2>
        <h3>
          {{currentQuestion.category}}
        </h3>
        <ul>
          <li v-for="answer in currentAnswers" :key="answer">
            <VButton
            :outlined="true"
            @click="onClick(answer)">
              {{answer}}
            </Vbutton>
          </li>
        </ul>
      </template>
  </div>
</template>

<script>
import axios from '@/packages/axios'
import shuffle from 'lodash.shuffle'
import VButton from '@/components/VButton'
export default {
  name: 'VQuestions',
  components: {
    VButton
  },
  data () {
    return {
      isRequesting: false,
      currentIndex: 0,
      questions: []
    }
  },
  computed: {
    currentQuestion () {
      if (this.questions.length) {
        return this.questions[this.currentIndex]
      }
      return null
    },
    currentAnswers () {
      const { currentQuestion } = this
      if (currentQuestion) {
        const answers = [
          ...currentQuestion.incorrect_answers, currentQuestion.correct_answer
        ]
        // console.log(answers)
        // console.log(currentQuestion.incorrect_answers)
        // console.log(currentQuestion.correct_answer)
        return shuffle(answers)
      }
      return []
    }
  },
  created () {
    this.fetchQuestions()
  },
  methods: {
    async fetchQuestions () {
      this.isRequesting = true
      try {
        const { data } = await axios.get('/api.php?amount=10')
        console.log(data)
        this.questions = data.results
        this.isRequesting = false
      } catch (error) {
        this.isRequesting = false
      }
    },
    onClick (answer) {
      const userChoice = answer
      console.log(userChoice)
      // console.log(this.currentQuestion.incorrect_answers)
      console.log(this.currentQuestion.correct_answer)
      // console.log(this.currentQuestion)
      if (userChoice === this.currentQuestion.correct_answer) {
        alert('ok')
        if (this.currentIndex++ + 1 === this.questions.length) {
          alert('LAIMEJAI NX')
        }
        console.log(this.questions.length)
        //   this.currentIndex++
      } else {
        alert('TU DURNAS')
      }
    }
  }
}
</script>

<style>
  .questions-wrapper {

    /* height: 100%; */
    background-color: #fff;
    margin: 0 20px;
    padding: 0;
    border-radius: 15px;
  }

  span {
    padding: 10px;
    font-size: 30px;
  }

  h2,
  h3 {
    padding: 0 20px;
  }

  h3 {
    font-size: 16px;
  }

  ul {
    padding: 0;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  li {
    margin: 8px 0;
    list-style-type: none;
  }
</style>
