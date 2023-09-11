<template>
  <div class="max-w-screen-sm mx-auto px-4 py-10">
    <!-- Status message -->
    <div v-if="statusMsg || errorMsg" class="mb-10 p-4 bg-light-grey rounded-md shadow-lg">
      <p class="text-at-light-green">
        {{ statusMsg }}
      </p>
      <p class="text-red-500">
        {{ errorMsg }}
      </p>
    </div>
    <!-- Consent write up -->
    <div class="max-w-screen-sm mx-auto px-4 py-10">
      <h2 class="text-3xl mb-8">Consent</h2>
      <h3 class="text-2xl mb-4">Read out the consent and click on the check boxes below</h3>
      <p class="text-l">
        Thank you for agreeing to do this questionnaire with us today. We’re going to work through
        the questions together to help you to figure out if you could benefit from any support and
        how best we can help with it. There might be some questions or areas you haven’t thought
        about before but as we ask them you might realise you could do with some help in that area.
        That’s totally fine and quite normal, the questionnaire is designed to identify all areas of
        need, including things you perhaps hadn’t considered before. There might be some questions
        that aren’t relevant to you; that’s ok too, you can just say it’s not relevant to you and
        we’ll just move on from those. Hopefully by the end we will have looked at every area of
        your life and you will have a full picture of the help you might benefit from. We will then
        support you to access the available help. We can’t guarantee that there will always be
        support for each area that is identified, but we will always do our best to find out what is
        available. You are in control of this process, you can stop the need assesment at any time
        and if there are any questions you don’t want to answer, just tell us and we can move on to
        the next one. These answers are kept securely, and we never share them or connect you to
        other places without your consent.
      </p>
    </div>
    <!-- Personal Consent-question -->
    <h1 class="text-3xl text-at-light-green mb-4">Personal details</h1>
    <div class="p-8 flex">
      <form
        @submit.prevent="recordPersonals"
        class="p-8 flex flex-col bg-light-grey rounded-md shadow-lg"
      >
        <div class="flex flex-col">
          <p class="text-2xl text-at-light-green">
            Are you happy to proceed with the needs assesment and allow us to stoe and use your
            information as described
          </p>
          <p class="text-2xl text-at-light-green"></p>
          <select
            @change="choiceChange"
            id="consent-Choice"
            class="mx-auto mt-8 p-2 text-gray-500 focus:outline-none"
            required
            v-model="consentChoice"
          >
            <option value="select-choice">Choose your choice</option>
            <option value="yes">Yes</option>
            <option value="no">No</option>
          </select>
        </div>

        <!-- Personal details section -->

        <div v-if="consentChoice === 'yes'" class="max-w-screen px-4 py-10">
          <div class="gap-y-2 relative" v-for="(item, index) in personals" :key="index">
            <div class="flex flex-col mb-2">
              <label for="firstName" class="mb-1 text-sm text-at-light-green">First Name</label>
              <input
                type="text"
                required
                class="p-2 w-full text-gray-500 focus:outline-none"
                v-model="item.firstName"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="lastName" class="mb-1 text-sm text-at-light-green">Last Name</label>
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.lastName"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="email" class="mb-1 text-sm text-at-light-green">Email</label>
              <input
                type="email"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.email"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="phoneNumber" class="mb-1 text-sm text-at-light-green">Phone number</label>
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.phoneNumber"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="address" class="mb-1 text-sm text-at-light-green">Address</label>
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.address"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="adultCount" class="mb-1 text-sm text-at-light-green"
                >Number of adults in household(18 and over)</label
              >
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.adultsCount"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="childrenCount" class="mb-1 text-sm text-at-light-green"
                >Number of children in household (under 18)</label
              >
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.childrenCount"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="dependantsCount" class="mb-1 text-sm text-at-light-green"
                >Number of additional dependants</label
              >
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.dependantsCount"
              />
            </div>
          </div>
          <button
            type="submit"
            class="mt-6 py-2 px-6 rounded-sm self-start text-sm text-white bg-at-light-green duration-200 border-solid border-2-transparent hover:border-at-light-green hover:bg-white hover:text-at-light-green"
          >
            Proceed
          </button>
        </div>

        <!--Financial details  -->
        <div class="flex flex-col">
          <p class="text-2xl text-at-light-green">
            The second section is looking at money and your financial needs. Would you be happy for
            us to ask you some questions about that
          </p>
          <p class="text-2xl text-at-light-green"></p>
          <select
            @change="financeChange"
            id="finance-Choice"
            class="mx-auto mt-8 p-2 text-gray-500 focus:outline-none"
            required
            v-model="financeChoice"
          >
            <option value="financeChoice">Choose your choice</option>
            <option value="yes">Yes</option>
            <option value="no">No</option>
          </select>
        </div>

        <div v-if="financeChoice === 'yes'" class="max-w-screen px-4 py-10">
          <div class="gap-y-2 relative" v-for="(item, index) in financial" :key="index">
            <div class="flex flex-col mb-2">
              <label for="connectChoice" class="mb-1 text-sm text-at-light-green"
                >If you find that you need help in this area, would you be happy for us to try to connect you to the appropriate place</label
              >
              <input
                type="text"
                required
                class="p-2 w-full text-gray-500 focus:outline-none"
                v-model="item.connectChoice"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="billsDifficulty" class="mb-1 text-sm text-at-light-green"
                >Do you ever have difficulty paying regular bills and for everyday needs</label
              >
              <input
                type="text"
                required
                class="p-2 w-full text-gray-500 focus:outline-none"
                v-model="item.billsDifficulty"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="helpDetails" class="mb-1 text-sm text-at-light-green"
                >Details of things I need help paying for</label
              >
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.helpDetails"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="debtDifficulties" class="mb-1 text-sm text-at-light-green"
                >Do you have any difficulty paying debts of fines or unexpected expense?</label
              >
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.debtDifficulties"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="budegtUse" class="mb-1 text-sm text-at-light-green"
                >Do you use a budget</label
              >
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.budgetUse"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="incomeSource" class="mb-1 text-sm text-at-light-green"
                >Which of the following best describe your income comes from</label
              >
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.incomeSource"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="others" class="mb-1 text-sm text-at-light-green"
                >If others(specify)</label
              >
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.others"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="support" class="mb-1 text-sm text-at-light-green"
                >Do you want help to find support for any of the following
              </label>
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.support"
              />
            </div>
          </div>
          <button
            @click="recordFinancials"
            type="button"
            class="mt-6 py-2 px-6 rounded-sm self-start text-sm text-white bg-at-light-green duration-200 border-solid border-2-transparent hover:border-at-light-green hover:bg-white hover:text-at-light-green"
          >
            Proceed
          </button>
        </div>

        <!-- Health needs -->
        <div v-if="healthChoice === 'yes'" class="max-w-screen px-4 py-10">
          <div class="gap-y-2 relative" v-for="(item, index) in health" :key="index">
            <div class="flex flex-col mb-2">
              <label for="docRegistration" class="mb-1 text-sm text-at-light-green"
                >Are you registered with a doctor</label
              >
              <input
                type="text"
                required
                class="p-2 w-full text-gray-500 focus:outline-none"
                v-model="item.docRegistration"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="dentistRegistration" class="mb-1 text-sm text-at-light-green"
                >Are you registered with a dentist</label
              >
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.dentistRegistration"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="accessHelp" class="mb-1 text-sm text-at-light-green"
                >Would you like help to access a doctor or a dentist</label
              >
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.accessHelp"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="healthRate" class="mb-1 text-sm text-at-light-green"
                >How would you rate your overall physical health</label
              >
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.healthRate"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="mentalHealth" class="mb-1 text-sm text-at-light-green"
                >How would you rate your overall mental health</label
              >
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.mentalHealth"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="sexualHealth" class="mb-1 text-sm text-at-light-green"
                >How would you rate your overall sexual health</label
              >
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.sexualHealth"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="dentalHealth" class="mb-1 text-sm text-at-light-green"
                >How would you rate your overall dental health</label
              >
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.dentalHealth"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="dietDescription" class="mb-1 text-sm text-at-light-green"
                >Which best describes your diet /eating (multiple tick is allowed)
              </label>
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.dietDescription"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="dependantsCount" class="mb-1 text-sm text-at-light-green"
                >Are you engaging with any help for any of the following
              </label>
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.dependantsCount"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="dependantsCount" class="mb-1 text-sm text-at-light-green"
                >Details (i.e support source etc)
              </label>
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.dependantsCount"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="dependantsCount" class="mb-1 text-sm text-at-light-green"
                >Would you like help accessing care for
              </label>
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.dependantsCount"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="dependantsCount" class="mb-1 text-sm text-at-light-green"
                >Would you like help accessing care for
              </label>
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.dependantsCount"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="dependantsCount" class="mb-1 text-sm text-at-light-green"
                >What area do you need help with
              </label>
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.dependantsCount"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="dependantsCount" class="mb-1 text-sm text-at-light-green"
                >Do you struggle with substance misuse or any addiction
              </label>
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.dependantsCount"
              />
            </div>
          </div>
          <button
            type="button"
            class="mt-6 py-2 px-6 rounded-sm self-start text-sm text-white bg-at-light-green duration-200 border-solid border-2-transparent hover:border-at-light-green hover:bg-white hover:text-at-light-green"
          >
            Proceed
          </button>
        </div>

        <!-- spiritual needs -->
        <div v-if="consentChoice === 'yes'" class="max-w-screen px-4 py-10">
          <div class="gap-y-2 relative" v-for="(item, index) in spiritual" :key="index">
            <div class="flex flex-col mb-2">
              <label for="firstName" class="mb-1 text-sm text-at-light-green"
                >Do you see yourself as a spiritual or religious person</label
              >
              <input
                type="text"
                required
                class="p-2 w-full text-gray-500 focus:outline-none"
                v-model="item.firstName"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="lastName" class="mb-1 text-sm text-at-light-green"
                >Do you have beliefs in line with any particular religion or faith community</label
              >
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.lastName"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="email" class="mb-1 text-sm text-at-light-green">Details </label>
              <input
                type="email"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.email"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="phoneNumber" class="mb-1 text-sm text-at-light-green"
                >Thinking about your level of involvement with your faith community, which of the
                following best describes you
              </label>
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.phoneNumber"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="address" class="mb-1 text-sm text-at-light-green"
                >Would you like help to be more involved with a faith community</label
              >
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.address"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="adultCount" class="mb-1 text-sm text-at-light-green">Details </label>
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.adultsCount"
              />
            </div>
          </div>
          <button
            type="submit"
            class="mt-6 py-2 px-6 rounded-sm self-start text-sm text-white bg-at-light-green duration-200 border-solid border-2-transparent hover:border-at-light-green hover:bg-white hover:text-at-light-green"
          >
            Proceed
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import { useRouter } from 'vue-router'
import { ref } from 'vue'
import { uid } from 'uid'
import { supabase } from '../supabase/supabase'
export default {
  name: 'PersonalView',
  setup() {
    // create variables
    const router = useRouter()
    const consentChoice = ref('select-choice')
    const financeChoice = ref('finance-choice')
    const statusMsg = ref(null)
    const errorMsg = ref(null)
    const personals = ref([])
    const financial = ref([])

    // check choice of consent form and display personal details if Yes
    const fillPersonal = () => {
      if (consentChoice.value === 'yes') {
        personals.value.push({
          id: uid(),
          firstName: '',
          lastName: '',
          email: '',
          phoneNumber: '',
          address: '',
          adultsCount: '',
          childrenCount: '',
          dependantsCount: ''
        })
        return
      }
    }

    // check choice of finance choice and display details if yes
    const fillFinance = () => {
        if (financeChoice.value === 'yes') {
            financial.value.push({
               connectChoice: '',
               billsDifficulty: '',
               helpDetails: '',
               debtDifficulties: '',
               budgetUse: '',
               incomeSource: '',
               others: '',
               support: '',
            })
            return
        }
    }

    // Listens for changes in the personal choice
    const choiceChange = () => {
      personals.value = []
      fillPersonal();
    }

    // Listens for change in finance choice
    const financeChange = () => {
        financial.value = []
        fillFinance();
    }

    // Record the personal details
    const recordPersonals = async () => {
      try {
        const { error } = await supabase.from('personals').insert([
          {
            personals: personals.value
          }
        ])
        if (error) throw error
        fillFinance();
        statusMsg.value = 'success: personal details submitted!'
        personals.value = []
        setTimeout(() => {
          statusMsg.value = false
        }, 5000)
      } catch (error) {
        errorMsg.value = `Error:${error.message}`
        setTimeout(() => {
          errorMsg.value = false
        }, 5000)
      }
    }

    // Record the financial details
    const recordFinancials = async () => {
      try {
        const { error } = await supabase.from('finance').insert([
          {
            financial: financial.value
          }
        ])
        if (error) throw error
        statusMsg.value = 'success: financial details submitted!'
        personals.value = []
        setTimeout(() => {
          statusMsg.value = false
        }, 5000)
      } catch (error) {
        errorMsg.value = `Error:${error.message}`
        setTimeout(() => {
          errorMsg.value = false
        }, 5000)
      }
    }

    return {
      errorMsg,
      consentChoice,
      personals,
      financial,
      financeChoice,
      statusMsg,
      choiceChange,
      fillPersonal,
      recordPersonals,
      fillFinance,
      financeChange,
      recordFinancials

    }
  }
}
</script>

<style></style>
