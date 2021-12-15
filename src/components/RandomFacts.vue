<script>
import axios from 'axios'

axios.defaults.baseURL = 'https://uselessfacts.jsph.pl'
export default {
  data: () => ({
    text: [],
    current: 0
  }),

  created() {
    axios.get(`${axios.defaults.baseURL}/random.json`).then((response) => {
      this.text.push(response.data.text)
    })
  },
  methods: {
    getFact() {
      if (!this.text[this.curent + 1]) {
        axios.get(`${axios.defaults.baseURL}/random.json`).then((response) => {
          this.text.push(response.data.text)
        })
      }
      this.current++
    }
  }
}
</script>

<template>
  <h1>Useless Facts</h1>
  <p>{{ text[current] }}</p>
  <div>
    <button :class="{ prev: current > 0, disable: current == 0 }" type="button" @click="current--">Prev</button>
    <button class="next" type="button" @click="getFact()">Next</button>
  </div>
</template>

<style scoped lang="sass">
h1
  font-family: Roboto
  font-size: 32px
  line-height: 37px
  position: absolute
  top: 15%
p
  font-family: Roboto
  font-style: italic
  font-weight: 300
  font-size: 24px
  line-height: 28px
  text-align: center
  position: absolute
  top: 35%
div
  position: absolute
  top: 65%
.prev
  background: rgba(27, 150, 91, 0.69)
.next
  background: rgba(71, 96, 224, 0.69)
.disable
  background: gray
  cursor: not-allowed
button
  border-radius: 5px
  border: none
  color: white
  font-weight: bold
  font-size: 14px
  line-height: 16px
  text-align: center
  padding: 10px 25px
  margin: 0 30px
</style>
