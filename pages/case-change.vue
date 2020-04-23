<template>
  <section class="section">
    <h2 class="title is-3 has-text-grey">Case Change</h2>
    <div class="columns is-touch">
      <div class="column">
        <b-field label="Text to convert" :label-position="labelPosition">
          <b-input class="something" v-model="textToChange" type="textarea"></b-input>
        </b-field>
      </div>
    </div>
    <div class="columns is-touch">
      <div class="column">
        <b-button @click="sentenceCase">Sentence case</b-button>
        <b-button @click="capitalCase">Capital case</b-button>
        <b-button @click="removeSymbols">Remove ':'</b-button>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      textToChange: ''
    }
  },
  methods: {
    firstLetterUpper(theString) {
      var newString = theString
        .toLowerCase()
        .replace(/(^\s*\w|[\.\!\?]\s*\w)/g, function(c) {
          return c.toUpperCase()
        })
      return newString
    },
    sentenceCase() {
      var theString = this.textToChange
      var newString = this.firstLetterUpper(theString)
      this.textToChange = newString
    },
    removeSymbols() {
      let text = this.textToChange
      text = text.replace(/:/g, '')
      this.textToChange = text
    },
    capitalCase() {
      const textArray = this.textToChange.split(' ');

      textArray.forEach((word,i)=>{
        textArray[i] = this.firstLetterUpper(word)
      });

      this.textToChange = textArray.join(' ')
    }
  }
}
</script>
<style lang="scss" scoped>
</style>