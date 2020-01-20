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

    <hr />
    <div class="columns is-touch">
      <div class="column">
        <div class="columns is-touch">
          <vue-json-pretty :path="'res'" :data="createdFields[0]" @click="handleClick"></vue-json-pretty>
        </div>
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
      createdFields: [],
      startingField: 100,
      fieldTitle: ''
    }
  },
  methods: {
    addField() {
      this.startingField += 10

      const slugTITLE = this.fieldTitle.replace(' ', '_').toLowerCase()
      const slugTITLEINDOFROMATION = slugTITLE + '_information_group'
      const TitleInformation = this.fieldTitle + ' Information'
      const slugTITLEDetails = slugTITLE + '_details'
      const slugTITLEAttachments = slugTITLE + '_upload'

      let objToAdd = {}
      objToAdd[slugTITLE] = {
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
        position: this.startingField + 1
      }

      objToAdd[slugTITLEINDOFROMATION] = {
        type: 'Group',
        items: {},
        title: TitleInformation,
        display: {
          width: 12,
          widget: {
            id: null
          }
        },
        position: this.startingField + 2
      }

      objToAdd[slugTITLEINDOFROMATION].items[slugTITLEDetails] = {
        type: 'String',
        title: this.fieldDescription,
        display: {
          width: 12,
          widget: {
            id: 'multiLine'
          }
        },
        position: this.startingField + 3
      }

      objToAdd[slugTITLEINDOFROMATION].items[slugTITLEAttachments] = {
        id: 'base.attachment',
        title: this.fieldUpload,
        display: {
          width: 12
        },
        position: this.startingField + 4
      }

      this.createdFields.push(objToAdd)
    }
  }
}
</script>





/*
      "paediatrician": {
        "type": "Boolean",
        "title": "Paediatrician",
        "display": {
          "width": 12,
          "widget": {
            "id": "radio",
            "layout": "horizontal"
          }
        },
        "options": [
          {
            "uuid": "bbb04d0a-26a8-47d2-8897-92d016761126",
            "title": "Yes",
            "value": true
          },
          {
            "uuid": "4cbf208d-d005-4c4f-bc2a-312bf960e805",
            "title": "No",
            "value": false
          }
        ],
        "position": 36,
        "validations": [
          {
            "message": "This field is required",
            "required": true
          }
        ]
      },
      "paediatrician_information_group": {
        "type": "Group",
        "items": {
          "paediatrician_details": {
            "type": "String",
            "title": "Please give details",
            "display": {
              "width": 12,
              "widget": {
                "id": "multiLine"
              }
            },
            "position": 37,
            "validations": [
              {
                "if": {
                  "==": [
                    {
                      "field": [
                        "detailed_applicant_information.paediatrician"
                      ]
                    },
                    true
                  ]
                },
                "message": "This field is required",
                "required": true
              }
            ]
          },
          "paediatrician_upload": {
            "id": "base.attachment",
            "title": "Please attach relevant documents",
            "display": {
              "width": 12
            },
            "position": 38,
            "validations": []
          }
        },
        "title": "Paediatrician Information",
        "display": {
          "width": 12,
          "conditions": [
            {
              "if": {
                "==": [
                  {
                    "field": [
                      "detailed_applicant_information.paediatrician"
                    ]
                  },
                  true
                ]
              },
              "action": {
                "visible": true
              }
            }
          ]
        },
        "position": 39,
        "validations": []
      },
      "psychiatrist": {
        "type": "Boolean",
        "title": "Psychiatrist",
        "display": {
          "width": 12,
          "widget": {
            "id": "radio",
            "layout": "horizontal"
          }
        },
        "options": [
          {
            "uuid": "4859f5a8-4be7-43e3-bc00-51f2350d45f8",
            "title": "Yes",
            "value": true
          },
          {
            "uuid": "28e2333e-7b44-4832-abd0-c63913df04de",
            "title": "No",
            "value": false
          }
        ],
        "position": 40,
        "validations": [
          {
            "message": "This field is required",
            "required": true
          }
        ]
      },
      "psychiatrist_information": {
        "type": "Group",
        "items": {
          "psychiatrist_give_details_2_1": {
            "type": "String",
            "title": "Please give details",
            "display": {
              "width": 12,
              "widget": {
                "id": "multiLine"
              }
            },
            "position": 41,
            "validations": [
              {
                "if": {
                  "==": [
                    {
                      "field": [
                        "detailed_applicant_information.psychiatrist"
                      ]
                    },
                    true
                  ]
                },
                "message": "This field is required",
                "required": true
              }
            ]
          },
          "psychiatrist_attach_relevant_documents_2": {
            "id": "base.attachment",
            "title": "Please attach relevant documents",
            "display": {
              "width": 12
            },
            "position": 42,
            "validations": []
          }
        },
        "title": "Psychiatrist Information",
        "display": {
          "width": 12,
          "widget": [],
          "conditions": [
            {
              "if": {
                "==": [
                  {
                    "field": [
                      "detailed_applicant_information.psychiatrist"
                    ]
                  },
                  true
                ]
              },
              "action": {
                "visible": true
              }
            }
          ]
        },
        "position": 43
      }, */