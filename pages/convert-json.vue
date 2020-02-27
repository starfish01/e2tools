<template>
  <section class="section">
    <h2 class="title is-3 has-text-grey">Convert old enrol JSON for new enrol</h2>
    <div class="columns is-touch">
      <div class="column">
        <b-field label="Text to convert">
          <b-input class="something" v-model="textToChange" type="textarea"></b-input>
        </b-field>
      </div>
    </div>
    <div class="columns is-touch">
      <div class="column">
        <b-button :disabled="!this.textToChange" @click="convertJson">Convert</b-button>
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
    convertJson() {
      try {
        let obj = JSON.parse(this.textToChange).options
      } catch {
        return
      }

      let newObj = []

      obj.forEach(element => {
        if (element.value !== '') {
          newObj.push({
            title: element.name,
            value: element.value
          })
        }
      })
      this.textToChange = JSON.stringify(newObj)
    }
  }
}
</script>
<style lang="scss" scoped>
</style>