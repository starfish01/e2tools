<template>
  <section class="section">
    <div class="columns is-touch">
      <div class="column">
        <b-field label="Title">
          <b-input v-model="fieldTitle"></b-input>
        </b-field>
      </div>
      <div class="column">
        <b-field label="Description">
          <b-input v-model="fieldDescription"></b-input>
        </b-field>
      </div>
      <div class="column">
        <b-field label="Upload">
          <b-input v-model="fieldUpload"></b-input>
        </b-field>
      </div>
      <div class="column">
        <b-field label="Starting Field Id">
          <b-input v-model="startingField"></b-input>
        </b-field>
      </div>
    </div>
    <b-button type="is-primary" @click="addField()">+</b-button>
    <b-button
      type="is-primary"
      v-clipboard:copy="JSON.stringify(objToAdd).slice(1, -1)"
      >Copy to clipboard</b-button
    >

    <hr />
    <div class="columns is-touch">
      <div class="column">
        <ol>
          <li v-for="item in this.addedItems" :key="item">{{ item }}</li>
        </ol>
      </div>
      <div class="column">
        <vue-json-pretty
          :deep="2"
          :path="'res'"
          :data="[objToAdd]"
        ></vue-json-pretty>
      </div>
    </div>
  </section>
</template>

<script>
import VueJsonPretty from 'vue-json-pretty'

export default {
  components: {
    VueJsonPretty
  },
  data() {
    return {
      fieldDescription: 'Please give details',
      fieldUpload: 'Please attach relevant documents',
      createdFields: {},
      startingField: 100,
      fieldTitle: '',
      objToAdd: {},
      addedItems: []
    }
  },
  methods: {
    addField() {
      this.startingField = parseInt(this.startingField) + 10

      const slugTITLE = this.fieldTitle.replace(' ', '_').toLowerCase()
      const slugTITLEINDOFROMATION = slugTITLE + '_information_group'
      const TitleInformation = this.fieldTitle + ' Information'
      const slugTITLEDetails = slugTITLE + '_details'
      const slugTITLEAttachments = slugTITLE + '_upload'

      this.addedItems.push(this.fieldTitle)
      this.addedItems = [...new Set(this.addedItems)]

      // Radio button
      this.objToAdd[slugTITLE] = {
        type: 'Boolean',
        title: this.fieldTitle,
        display: {
          width: 12,
          widget: {
            id: 'radio',
            layout: 'horizontal'
          }
        },
        options: [
          {
            title: 'Yes',
            value: true
          },
          {
            title: 'No',
            value: false
          }
        ],
        position: this.startingField + 1,
        validations: [
          {
            message: 'This field is required ',
            required: true
          }
        ]
      }

      // Group
      this.objToAdd[slugTITLEINDOFROMATION] = {
        type: 'Group',
        items: {},
        title: TitleInformation,
        display: {
          width: 12,
          widget: []
        },
        position: this.startingField + 2,
        validations: [
          {
            if: {
              '==': [
                {
                  field: [slugTITLE]
                },
                true
              ]
            },
            message: 'This field is required',
            required: true
          }
        ]
      }

      // Details
      this.objToAdd[slugTITLEINDOFROMATION].items[slugTITLEDetails] = {
        type: 'String',
        title: this.fieldDescription,
        display: {
          width: 12,
          widget: {
            id: 'multiLine'
          }
        },
        position: this.startingField + 3,
        validations: [
          {
            if: {
              '==': [
                {
                  field: [slugTITLE]
                },
                true
              ]
            },
            message: 'This field is required',
            required: true
          }
        ]
      }

      // Upload Files
      this.objToAdd[slugTITLEINDOFROMATION].items[slugTITLEAttachments] = {
        id: 'base.attachment',
        title: this.fieldUpload,
        display: {
          width: 12
        },
        position: this.startingField + 4,
        validations: [
          {
            if: {
              '==': [
                {
                  field: [slugTITLE]
                },
                true
              ]
            },
            message: 'This field is required',
            required: true
          }
        ]
      }
    }
  },
  computed: {}
}
</script>
