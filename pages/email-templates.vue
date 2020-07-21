<template>
  <section class="section">
    <h2 class="title is-3 has-text-grey">Email Templates</h2>
    <h2 class="subtitle">
      <a
        href="https://digistorm.atlassian.net/wiki/spaces/IP/pages/17858645/Default+Text"
        target="_blank"
      >More Information</a>
    </h2>
    <div class="columns is-touch">
      <div class="column">
        <b-field label="School Name">
          <b-input v-model="schoolName"></b-input>
        </b-field>
      </div>
      <div class="column">
        <b-field label="Email">
          <b-input v-model="schoolEmail"></b-input>
        </b-field>
      </div>
      <div class="column">
        <b-field label="Phone">
          <b-input v-model="schoolPhone"></b-input>
        </b-field>
      </div>
    </div>
    <div class="columns is-touch">
      <div class="column">
        <b-field label="Form Title">
          <b-input v-model="formType"></b-input>
        </b-field>
      </div>
    </div>
    <hr />
    <div class="columns is-multiline is-touch">
      <div v-for="(email,index) in emails" :key="index" class="column is-one-quarter">
        <b-button @click="displayEmail(email)">{{email.title}}</b-button>
      </div>
    </div>
    <hr />
    <div class="columns is-multiline">
      <div class="column is-full">
        <b-field label="Name">
          <b-input v-model="subjectLine"></b-input>
        </b-field>
      </div>
      <div class="column is-full">
        <b-field label="Message">
          <b-input v-model="emailbody" type="textarea"></b-input>
        </b-field>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      formType: 'enrolment application',
      schoolName: '',
      schoolEmail: '',
      schoolPhone: '',
      subjectLine: '',
      emailbody: '',
      emails: [
        {
          title: 'Enrolment Completion',
          subject: '{{schoolname}} | {{formType}} Completed',
          email: `Dear {guardian:get_name()},

Thank you for expressing an interest in joining the {{schoolname}} community.

Please find attached a summary of the information that you have provided as well as a receipt for your {{formType}} fee.

One of our Admissions staff will be in touch shortly to discuss the next steps.

If you have any questions about your {{formType}}, please contact the Admissions Team.

T: {{phone}}
E: {{email}}

{{schoolname}}`
        },
        {
          title: 'Enrolment Reminder Email',
          subject: '{{schoolname}} | {{formType}} Reminder',
          email: `Dear {guardian:get_name()},

We noticed that you have not completed the {{formType}} for {{schoolname}}.

You can continue your {{schoolname}} at any time by clicking the link in the button below.

– Button object (Resume Application)–

If there is anything that we can be of assistance with, please feel free to contact us.

Kind Regards,
Enrolments`
        }
      ]
    }
  },
  methods: {
    displayEmail(emailData) {
      let outputEmailbody = emailData.email
      let outputSubjectLine = emailData.subject

      let uppercaseFormType = this.titleCase(this.formType);

      outputSubjectLine = outputSubjectLine
        .split('{{schoolname}}')
        .join(this.schoolName)

      outputSubjectLine = outputSubjectLine
        .split('{{formType}}')
        .join(uppercaseFormType)

      outputEmailbody = outputEmailbody
        .split('{{schoolname}}')
        .join(this.schoolName)
      outputEmailbody = outputEmailbody
        .split('{{phone}}')
        .join(this.schoolPhone)
      outputEmailbody = outputEmailbody
        .split('{{email}}')
        .join(this.schoolEmail)

      outputEmailbody = outputEmailbody
        .split('{{formType}}')
        .join(this.formType)

      this.subjectLine = outputSubjectLine
      this.emailbody = outputEmailbody
    },
    titleCase(str) {
      let splitStr = str.toLowerCase().split(' ')
      for (var i = 0; i < splitStr.length; i++) {
        // You do not need to check if i is larger than splitStr length, as your for does that for you
        // Assign it back to the array
        splitStr[i] =
          splitStr[i].charAt(0).toUpperCase() + splitStr[i].substring(1)
      }
      // Directly return the joined string
      return splitStr.join(' ');
    }
  }
}
</script>
<style lang="scss" scoped>
</style>
