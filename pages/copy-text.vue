<template>
  <section class="section">
    <h2 class="title is-3 has-text-grey">Copy Snippts</h2>
    <div class="columns is-touch is-multiline">
      <div class="column">
        <div class="card">
          <div class="card-content">
            <div class="content">
              <div class="columns is-touch" v-for="(item, index) in buttons" :key="index">
                <div >
                  <h3>{{ item.title }}</h3>
                  <ul>
                    <b-button style="margin-bottom:5px" v-for="(button,i) in item.items" :key="i" v-clipboard:copy="button.text" @click="copiedItem()">{{button.title}}</b-button>
                  </ul>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="column is-6">
        <div class="card">
          <div class="card-content">
            <div class="media">
              <div class="media-content">
                <p class="title is-4">One Password Set up</p>
              </div>
            </div>
            <div class="content">
              <div class="columns is-touch">
                <b-field class="column is-6" label="School Name">
                  <b-input v-model="onePass.schoolName"></b-input>
                </b-field>
                <b-field class="column is-6" label="School Code">
                  <b-input v-model="onePass.schoolCode"></b-input>
                </b-field>
              </div>
              <div class="columns is-touch" style="justify-content: space-around">
                <b-button
                  v-clipboard:copy="onePass.schoolName + ' | ' + onePass.schoolCode + ' | eduSTACK'"
                >Title</b-button>
                <b-button v-clipboard:copy="onePass.schoolCode + '@digistorm.com'">Email</b-button>
                <b-button v-clipboard:copy="onePass.schoolCode + '.app.digistorm.com'">Website</b-button>
                <b-button v-clipboard:copy="'app.digistorm.com'">Website2</b-button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      onePass: {
        schoolName: '',
        schoolCode: '',
        username: ''
      },
      buttons: [
        {
          title: 'Guardian Page',
          items: [
            {
              title: 'Occupation group data',
              text: `<p><strong>Group 1: </strong></p> <p>Senior management in large business organisation government administration and defence and qualified professionals. </p> <p> Senior executive/manager/department head in industry, commerce, media or other large organisation.</p> <p> Public service manager (section head or above), regional director, health/education/police/fire services administrator.</p> <p> Other administrator (school principal, faculty head/dean, library/museum/gallery director, research facility director).</p> <p> Defence Forces commissioned officer.</p> <p> Professionals generally have degree or higher qualifications and experience in applying this knowledge to design, develop or operate complex systems; identify, treat and advise on problems; and teach others.</p> <p> Health, education, law, social welfare, engineering, science, computing professional.</p> <p> Business (management consultant, business analyst, accountant, auditor, policy analyst, actuary, valuer).</p> <p> Air/sea transport (aircraft/ship’s captain/officer/pilot, flight officer, flying instructor, air traffic controller).</p> <p>&nbsp;</p> <p><strong>Group 2: </strong></p> <p>Other business managers, arts/media/sportspersons and associate professionals.</p> <p> Owner/manager of farm, construction, import/export, wholesale, manufacturing, transport, real estate business.</p> <p> Specialist manager (finance/engineering/production/personnel/industrial relations/sales/marketing).</p> <p> Financial services manager (bank branch manager, finance/investment/insurance broker, credit/loans officer).</p> <p> Retail sales/services manager (shop, petrol station, restaurant, club, hotel/motel, cinema, theatre, and agency). </p> <p> Arts/media/sports (musician, actor, dancer, painter, potter, sculptor, journalist, author, media presenter, photographer, designer, illustrator, proof reader, sportsman/woman/ coach, trainer, sports official).</p> <p> Associate professionals generally have diploma/technical qualifications and support managers and professionals.</p> <p> Health, education, law, social welfare, engineering, science, computing technician/associate professional.</p> <p> Business/administration (recruitment/employment/industrial relations/training officer, marketing/advertising specialist, market research analyst, technical sales representative, retail buyer, office/project manager).</p> <p> Defence Forces senior non-commissioned officer.</p> <p>&nbsp;</p> <p><strong>Group 3: </strong></p> <p>Tradesmen/women, clerks and skilled office, sales and service staff.</p> <p> Tradesmen/women generally have completed a four-year trade certificate, usually by apprenticeship. All tradesmen/women are included in this group.</p> <p> Clerks (bookkeeper, bank/PO clerk, statistical/actuarial clerk, accounting/claims/audit clerk, payroll clerk, recording/ registry/filing clerk, betting clerk, stores/inventory clerk, purchasing/order clerk, freight/transport/ shipping clerk, bond clerk, customs agent, customer services clerk, admissions clerk).</p> <p> Skilled office, sales and service staff.</p> <p> Office (secretary, personal assistant, desktop publishing operator, switchboard operator).</p> <p> Sales (company sales representative, auctioneer, insurance agent/assessor/loss adjuster, market researcher).</p> <p> Service (aged/disabled/refuge/child care worker, nanny, meter reader, parking inspector, postal worker, courier, travel agent, tour guide, flight attendant, fitness instructor, casino dealer/supervisor).</p> <p>&nbsp;</p> <p><strong>Group 4:</strong> </p> <p>Machine operators, hospitality staff, assistants, labourers and related workers.</p> <p> Drivers, mobile plant, production/processing machinery and other machinery operators.</p> <p> Hospitality staff (hotel service supervisor, receptionist, waiter, bar attendant, kitchen hand, porter, and housekeeper).</p> <p> Office assistants, sales assistants and other assistants.</p> <p> Office (typist, word processing/data entry/business machine operator, receptionist, office assistant).</p> <p> Sales (sales assistant, motor vehicle/caravan/parts salesperson, checkout operator, cashier, bus/train conductor, ticket seller, service station attendant, car rental desk staff, street vendor, telemarketer, shelf stacker).</p> <p> Assistant/aide (trades’ assistant, school/teacher’s aide, dental assistant, veterinary nurse, nursing assistant, museum/ gallery attendant, usher, home helper, saloon assistant, animal attendant).</p> <p> Labourer and related workers.</p> <p> Defence forces ranks below senior NCO not included above.</p> <p> Agriculture, horticulture, forestry, fishing, mining worker (farm overseer, shearer, wool/hide classer, farm hand, horse trainer, nurseryman, greenkeeper, gardener, tree surgeon, forestry/logging worker, miner, seafarer/fishing hand).</p> <p> Other worker (labourer, factory hand, storeman, guard, cleaner, caretaker, laundry worker, trolley collector, car park attendant, crossing supervisor).</p> <p>&nbsp;</p> <p><strong>Group 8:</strong></p> <p>A person has not been in paid work in the last 12 months.</p>`
            },
            {
              title: 'Parent Acknowlegement',
              text:
                'I/We acknowledge that all legal guardians and carers for the student have been entered into this application'
            }
          ]
        },
        {
          title: 'Confirmation',
          items: [
            {
              title: 'Confirmation of details',
              text: 'I/We confirm that the information given in this form is true, complete and accurate'
            }
          ]
        },
        {
          title: 'Non Form',
          items: [
            {
              title: 'Complete Page Text',
              text: 'Thank you, you’ll hear from one of our staff shortly.'
            },
            {
               title: 'CSS for tables',
              text: "table class='digi-table' style='font-weight:bold; width:100%'"
            }
          ]
        }
      ]
    }
  },
  methods: {
    copiedItem() {
      this.$buefy.toast.open('Copied to clip board')
    }
  }
}
</script>
<style lang="scss" scoped>
</style>
