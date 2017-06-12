<template>
  <div class='container'>
    <div class='columns'>
      <div class="column col-6">
        <div class="form-group">
          <input class="form-input" ref='input' type="text" v-model="input" placeholder="Enter word here..." />
        </div>
        <blockquote>
          <p>
            <span class='word' v-for='item in textArray' :class='{"active": item.active}'>{{ item.word }} </span>
          </p>
          <cite>- Bill Gates</cite>
        </blockquote>
        <button class='btn btn-primary' @click='startWatcher()' ref='button'>Start Test</button>
        <div v-if='typeof wpm === "number"' class="empty">
          <div class="empty-icon">
            <i class="icon icon-check"></i>
          </div>
          <h4 class="empty-title">Congratulations</h4>
          <p class="empty-subtitle">You type <span style='color:#5764c6'>{{wpm}}</span> words per minute!</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'typing-area',
  data () {
    return {
      input: '',
      text: 'The advance of technology is based on making it fit in so that you don\'t really even notice it, so it\'s part of everyday life.',
      currentWord: 'The ',
      currentWordIndex: 0,
      interval: null,
      totalSeconds: 0,
      start: false,
      wpm: null
    }
  },
  watch: {
    input () {
      if (this.start) {
        if (this.input === this.currentWord) {
          if (this.currentWordIndex === this.textArray.length - 1) {
            this.stopWatcher()
          } else {
            this.input = ''
            this.currentWordIndex++
            this.currentWord = this.textArray[this.currentWordIndex].word
          }
        }
      }
    }
  },
  methods: {
    startWatcher () {
      this.start = true
      this.$refs.input.focus()
      this.$refs.button.classList.add('loading')
      this.interval = setInterval(() => {
        this.totalSeconds++
      }, 1000)
    },
    stopWatcher () {
      this.start = false
      this.$refs.button.classList.remove('loading')
      clearInterval(this.interval)
      this.wpm = Math.round((this.text.split(' ').length / this.totalSeconds) * 60)
    }
  },
  computed: {
    textArray () {
      return this.text.split(' ').map((word, index) => {
        if (index !== this.text.split(' ').length - 1) {
          return {
            word: `${word} `,
            active: `${word} ` === this.currentWord && index === this.currentWordIndex
          }
        } else {
          return {
            word: word,
            active: word === this.currentWord && index === this.currentWordIndex
          }
        }
      })
    }
  }
}
</script>

<style scoped>
.columns {
  justify-content: center;
}
.btn {
  margin: 5px 0;
}
.word.active {
  color: #5764c6;
  font-weight: bold;
}
</style>
