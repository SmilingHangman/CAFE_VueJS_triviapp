<template>
  <div class="quizz-app" id="app">
    <h1 v-if="!started">TriviAPP</h1>
    <VButton
      v-if="!started"
      :outlined="false"
      @click="onClick">
      Start
    </VButton>
    <VQuestions v-if="started" v-on:changeStarted="updateStarted($event)">
    </VQuestions>
  </div>
</template>

<script>
import VButton from '@/components/VButton'
import VQuestions from '@/components/VQuestions'
export default {
  name: 'App',
  components: {
    VButton,
    VQuestions
  },
  data () {
    return {
      started: false
    }
  },
  methods: {
    onClick () {
      this.started = true
    },
    updateStarted: function (event) {
      this.started = event
    }
  }
}
</script>

<style>
  .quizz-app {
    width: 375px;
    height: 600px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 20px 0;
    background-color: #fff;
    background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='100%25' height='100%25' %3E%3Cdefs%3E%3ClinearGradient id='a' x1='0' x2='0' y1='0' y2='1' gradientTransform='rotate(302,0.5,0.5)'%3E%3Cstop offset='0' stop-color='%2380F'/%3E%3Cstop offset='1' stop-color='%23f40'/%3E%3C/linearGradient%3E%3C/defs%3E%3Cpattern id='b' width='34' height='34' patternUnits='userSpaceOnUse'%3E%3Ccircle fill='%23ffffff' cx='17' cy='17' r='17'/%3E%3C/pattern%3E%3Crect width='100%25' height='100%25' fill='url(%23a)'/%3E%3Crect width='100%25' height='100%25' fill='url(%23b)' fill-opacity='0.2'/%3E%3C/svg%3E");
    background-attachment: fixed;
    background-size: cover;
  }

  h1 {
    margin: 60% 0 70% 0;
    font-family: fantasy;
    color: #fff;
    transform: rotate(-15deg);
    font-size: 44px;
    text-shadow: 5px 4px 1px rgb(45, 12, 66);
  }
</style>
