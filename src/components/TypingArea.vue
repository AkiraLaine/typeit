<template>
  <div class='container'>
    <div class='columns'>
      <div class="column col-6">
        <div class="form-group">
          <input class="form-input" type="text" id="input" placeholder="Enter word here..." />
        </div>
        <blockquote>
          <p>The advance of technology is based on making it fit in so that you don't really even notice it, so it's part of everyday life. </p>
          <cite>- Bill Gates</cite>
        </blockquote>
        <button class='btn btn-primary' @click='startWatcher()' ref='button'>Start Test</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'typing-area',
  data () {
    return {
      word: '',
      text: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit.',
      currentText: 'Lorem',
      interval: null,
      totalSeconds: 0,
      start: false
    }
  },
  watch: {
    word () {
      if (this.start) {
        if (this.word === this.currentText) {
          const currentTextIndex = this.text.split(' ').indexOf(this.currentText)
          if (currentTextIndex === this.text.split(' ').length - 1) this.stopWatcher()
          else {
            this.word = ''
            this.currentText = this.text.split(' ')[currentTextIndex + 1]
          }
        }
      }
    }
  },
  methods: {
    startWatcher () {
      this.start = true
      this.$refs.button.classList.add('loading')
      this.interval = setInterval(() => {
        this.totalSeconds++
      }, 1000)
    },
    stopWatcher () {
      this.start = false
      this.$refs.button.classList.remove('loading')
      clearInterval(this.interval)
      console.log((this.text.split(' ').length / this.totalSeconds) * 60)
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
</style>
