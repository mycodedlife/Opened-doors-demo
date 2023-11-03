<template>
  <div class="max-w-screen-sm mx-auto px-4 py-10">
    <!-- Consent write up -->
    <div class="max-w-screen-sm mx-auto px-4 py-10">
      <h2 class="text-3xl mb-8">Consent</h2>
      <h3 class="text-2xl mb-4">
        Read out the consent and select your appropriate choice for each section
      </h3>
      <p class="text-l">
        Thank you for agreeing to do this questionnaire with us today. We are going to work through
        the questions together to help you to figure out if you could benefit from any support and
        how best we can help with it. We can not guarantee that there will always be support for
        each area that is identified, but we will always do our best to find out what is available.
        You are in control of this process, you can stop the need assesment at any time and if there
        are any questions you dont want to answer, just tell us and we can move on to the next one.
        These answers are kept securely, and we never share them or connect you to other places
        without your consent.
      </p>
      <p class="mt-16">
        There might be some questions or areas you have not thought about before but as we ask them
        you might realise you could do with some help in that area. That is totally fine and quite
        normal, the questionnaire is designed to identify all areas of need, including things you
        perhaps had not considered before. There might be some questions that are not relevant to
        you; that is ok too, you can just say it is not relevant to you and we will just move on
        from those. Hopefully by the end we will have looked at every area of your life and you will
        have a full picture of the help you might benefit from. We will then support you to access
        the available help.
      </p>
    </div>
    <!-- Personal Consent-question -->

    <div class="p-8 flex">
      <!-- Status message -->
      <div v-if="statusMsg || errorMsg" class="status-message flex mb-10 mx-auto p-4 bg-light-grey shadow-lg">        
        <div class="image-container">
          <img src="https://cdn.pixabay.com/photo/2023/03/30/00/21/check-7886573_640.png" alt="" />
        </div>
        
        <p class="text-at-light-green">
          {{ statusMsg }}
        </p>
        <p class="text-red-500">
          {{ errorMsg }}
        </p>
      </div>
      <form @submit.prevent="finish" class="p-8 flex flex-col bg-light-grey rounded-md shadow-lg">
        <div class="flex flex-col mb-8">
          <h1 class="text-3xl text-at-light-green mb-4">Personal details</h1>
          <p class="text-2xl ">
            Are you happy to proceed with the needs assesment and allow us to store and use your
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
            @click="recordPersonals"
            type="button"
            class="mt-6 py-2 px-6 rounded-sm self-start text-sm text-white bg-at-light-green duration-200 border-solid border-2-transparent hover:border-at-light-green hover:bg-white hover:text-at-light-green"
          >
            Proceed
          </button>
        </div>
        <hr />
        <!--Financial consent  -->
        <div class="flex flex-col mt-8 mb-8">
          <h1 class="text-3xl text-at-light-green mb-4">Financial details</h1>
          <p class="text-2xl ">
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

        <!-- Financial details section -->
        <div v-if="financeChoice === 'yes'" class="max-w-screen px-4 py-10">
          <div class="gap-y-2 relative" v-for="(item, index) in financials" :key="index">
            <div class="flex flex-col mb-2">
              <label for="connectChoice" class="mb-1 text-sm text-at-light-green"
                >If you find that you need help in this area, would you be happy for us to try to
                connect you to the appropriate place</label
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

        <hr />
        <!--Health consent  -->
        <div class="flex flex-col mt-8 mb-8">
          <h1 class="text-3xl text-at-light-green mb-4">Health details</h1>
          <p class="text-2xl ">
            The third section will be looking at your physical, mental and emotional health needs.
            Would you be happy for us to ask you some questions about that
          </p>
          <p class="text-2xl text-at-light-green"></p>
          <select
            @change="healthChange"
            id="health-Choice"
            class="mx-auto mt-8 p-2 text-gray-500 focus:outline-none"
            required
            v-model="healthChoice"
          >
            <option value="healthChoice">Choose your choice</option>
            <option value="yes">Yes</option>
            <option value="no">No</option>
          </select>
        </div>

        <!-- Health needs questions -->
        <div v-if="healthChoice === 'yes'" class="max-w-screen px-4 py-10">
          <div class="gap-y-2 relative" v-for="(item, index) in healths" :key="index">
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
              <label for="supportSource" class="mb-1 text-sm text-at-light-green"
                >Are you engaging with any help for any of the following
              </label>
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.engagingHelp"
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
                v-model="item.supportSource"
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
                v-model="item.accessingCare"
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
                v-model="item.areaHelp"
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
                v-model="item.substanceStruggle"
              />
            </div>
          </div>
          <button
            @click="recordHealth"
            type="button"
            class="mt-6 py-2 px-6 rounded-sm self-start text-sm text-white bg-at-light-green duration-200 border-solid border-2-transparent hover:border-at-light-green hover:bg-white hover:text-at-light-green"
          >
            Proceed
          </button>
        </div>
        <hr />

        <!--Spiritual consent  -->
        <div class="flex flex-col mt-8 mb-8">
          <h1 class="text-3xl text-at-light-green mb-4">Spiritual details</h1>
          <p class="text-2xl ">
            This section will be looking at your spiritual needs. Would you be happy for us to ask
            you some questions about that . Would you be happy for us to ask you some questions
            about that
          </p>
          <p class="text-2xl text-at-light-green"></p>
          <select
            @change="spiritualChange"
            id="spiritual-Choice"
            class="mx-auto mt-8 p-2 text-gray-500 focus:outline-none"
            required
            v-model="spiritualChoice"
          >
            <option value="spiritualChoice">Choose your choice</option>
            <option value="yes">Yes</option>
            <option value="no">No</option>
          </select>
        </div>

        <!-- spiritual needs -->
        <div v-if="spiritualChoice === 'yes'" class="max-w-screen px-4 py-10">
          <div class="gap-y-2 relative" v-for="(item, index) in spirituals" :key="index">
            <div class="flex flex-col mb-2">
              <label for="firstName" class="mb-1 text-sm text-at-light-green"
                >Do you see yourself as a spiritual or religious person</label
              >
              <input
                type="text"
                required
                class="p-2 w-full text-gray-500 focus:outline-none"
                v-model="item.spiritualOrReligious"
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
                v-model="item.religiousBeliefs"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="email" class="mb-1 text-sm text-at-light-green">Details </label>
              <input
                type="email"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.beliefDetails"
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
                v-model="item.faithLevel"
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
                v-model="item.faithInvolvement"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="adultCount" class="mb-1 text-sm text-at-light-green">Details </label>
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.involvmentDetails"
              />
            </div>
          </div>
          <button
            @click="recordSpiritual"
            type="button"
            class="mt-6 py-2 px-6 rounded-sm self-start text-sm text-white bg-at-light-green duration-200 border-solid border-2-transparent hover:border-at-light-green hover:bg-white hover:text-at-light-green"
          >
            Proceed
          </button>
        </div>

        <hr />
        <!--Practical consent  -->
        <div class="flex flex-col mt-8 mb-8">
          <h1 class="text-3xl text-at-light-green mb-4">Practical details</h1>
          <p class="text-2xl ">
            This section will be looking at your practical needs. Would you be happy for us to ask
            you some questions about that . Would you be happy for us to ask you some questions
            about that
          </p>
          <p class="text-2xl text-at-light-green"></p>
          <select
            @change="practicalChange"
            id="practical-Choice"
            class="mx-auto mt-8 p-2 text-gray-500 focus:outline-none"
            required
            v-model="practicalChoice"
          >
            <option value="spiritualChoice">Choose your choice</option>
            <option value="yes">Yes</option>
            <option value="no">No</option>
          </select>
        </div>

        <!-- Practical needs -->
        <div v-if="practicalChoice === 'yes'" class="max-w-screen px-4 py-10">
          <div class="gap-y-2 relative" v-for="(item, index) in practicals" :key="index">
            <div class="flex flex-col mb-2">
              <label for="firstName" class="mb-1 text-sm text-at-light-green"
                >If you find that you need help in this area, would you be happy for us to try to
                connect you to the appropriate place</label
              >
              <input
                type="text"
                required
                class="p-2 w-full text-gray-500 focus:outline-none"
                v-model="item.needConnect"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="lastName" class="mb-1 text-sm text-at-light-green"
                >Would you like help to access support for any of the following areas</label
              >
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.supportArea"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="email" class="mb-1 text-sm text-at-light-green">Details </label>
              <input
                type="email"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.details"
              />
            </div>

            <button
              @click="recordPractical"
              type="button"
              class="mt-6 py-2 px-6 rounded-sm self-start text-sm text-white bg-at-light-green duration-200 border-solid border-2-transparent hover:border-at-light-green hover:bg-white hover:text-at-light-green"
            >
              Proceed
            </button>
          </div>
        </div>

        <hr />
        <!--Accomodation consent  -->
        <div class="flex flex-col mt-8 mb-8">
          <h1 class="text-3xl text-at-light-green mb-4">Accomodation details</h1>
          <p class="text-2xl">
            This section will be looking at your employment needs. Would you be happy for us to ask
            you some questions about that . Would you be happy for us to ask you some questions
            about that
          </p>
          <p class="text-2xl text-at-light-green"></p>
          <select
            @change="accomodationChange"
            id="accomodation-Choice"
            class="mx-auto mt-8 p-2 text-gray-500 focus:outline-none"
            required
            v-model="accomodationChoice"
          >
            <option value="accomodationChoice">Choose your choice</option>
            <option value="yes">Yes</option>
            <option value="no">No</option>
          </select>
        </div>

        <!-- Accomodation needs -->
        <div v-if="accomodationChoice === 'yes'" class="max-w-screen px-4 py-10">
          <div class="gap-y-2 relative" v-for="(item, index) in accomodations" :key="index">
            <div class="flex flex-col mb-2">
              <label for="firstName" class="mb-1 text-sm text-at-light-green"
                >If you find that you need help in this area, would you be happy for us to try to
                connect you to the appropriate place</label
              >
              <input
                type="text"
                required
                class="p-2 w-full text-gray-500 focus:outline-none"
                v-model="item.needConnect"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="lastName" class="mb-1 text-sm text-at-light-green"
                >Are you happy with your accomodation</label
              >
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.accomodationChoice"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="email" class="mb-1 text-sm text-at-light-green"
                >Which of the following best describes your accommodation situation
              </label>
              <input
                type="email"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.accomodationSituation"
              />
            </div>

            <div class="flex flex-col mb-2">
              <label for="email" class="mb-1 text-sm text-at-light-green">Details </label>
              <input
                type="email"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.details"
              />
            </div>

            <button
              @click="recordAccomodation"
              type="button"
              class="mt-6 py-2 px-6 rounded-sm self-start text-sm text-white bg-at-light-green duration-200 border-solid border-2-transparent hover:border-at-light-green hover:bg-white hover:text-at-light-green"
            >
              Proceed
            </button>
          </div>
        </div>

        <hr />
        <!--Employability consent  -->
        <div class="flex flex-col mt-8 mb-8">
          <h1 class="text-3xl text-at-light-green mb-4">Employment details</h1>
          <p class="text-2xl ">
            This section will be looking at your employment needs. Would you be happy for us to ask
            you some questions about that . Would you be happy for us to ask you some questions
            about that
          </p>
          <p class="text-2xl text-at-light-green"></p>
          <select
            @change="employmentChange"
            id="employment-Choice"
            class="mx-auto mt-8 p-2 text-gray-500 focus:outline-none"
            required
            v-model="employmentChoice"
          >
            <option value="employmentChoice">Choose your choice</option>
            <option value="yes">Yes</option>
            <option value="no">No</option>
          </select>
        </div>

        <!-- Employability needs -->
        <div v-if="employmentChoice === 'yes'" class="max-w-screen px-4 py-10">
          <div class="gap-y-2 relative" v-for="(item, index) in employments" :key="index">
            <div class="flex flex-col mb-2">
              <label for="firstName" class="mb-1 text-sm text-at-light-green"
                >If you find that you need help in this area, would you be happy for us to try to
                connect you to the appropriate place</label
              >
              <input
                type="text"
                required
                class="p-2 w-full text-gray-500 focus:outline-none"
                v-model="item.needConnect"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="lastName" class="mb-1 text-sm text-at-light-green"
                >Thinking about your employment situation, which of these best describes your
                situation?</label
              >
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.employmentSituation"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="email" class="mb-1 text-sm text-at-light-green">Details </label>
              <input
                type="email"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.details"
              />
            </div>

            <button
              @click="recordEmployment"
              type="button"
              class="mt-6 py-2 px-6 rounded-sm self-start text-sm text-white bg-at-light-green duration-200 border-solid border-2-transparent hover:border-at-light-green hover:bg-white hover:text-at-light-green"
            >
              Proceed
            </button>
          </div>
        </div>

        <hr />
        <!--Education and training needs consent-->
        <div class="flex flex-col mt-8 mb-8">
          <h1 class="text-3xl text-at-light-green mb-4">Education details</h1>
          <p class="text-2xl ">
            This section will be looking at your education and training needs. Would you be happy
            for us to ask you some questions about that . Would you be happy for us to ask you some
            questions about that
          </p>
          <p class="text-2xl text-at-light-green"></p>
          <select
            @change="educationChange"
            id="education-Choice"
            class="mx-auto mt-8 p-2 text-gray-500 focus:outline-none"
            required
            v-model="educationChoice"
          >
            <option value="educationChoice">Choose your choice</option>
            <option value="yes">Yes</option>
            <option value="no">No</option>
          </select>
        </div>

        <!-- Education and training needs -->
        <div v-if="educationChoice === 'yes'" class="max-w-screen px-4 py-10">
          <div class="gap-y-2 relative" v-for="(item, index) in educations" :key="index">
            <div class="flex flex-col mb-2">
              <label for="firstName" class="mb-1 text-sm text-at-light-green"
                >If you find that you need help in this area, would you be happy for us to try to
                connect you to the appropriate place</label
              >
              <input
                type="text"
                required
                class="p-2 w-full text-gray-500 focus:outline-none"
                v-model="item.needConnect"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="lastName" class="mb-1 text-sm text-at-light-green"
                >Are you looking for any educational or training opportunities</label
              >
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.trainingOpportunities"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="email" class="mb-1 text-sm text-at-light-green"
                >Would you like help to access vocational training courses</label
              >
              <input
                type="email"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.accessCourses"
              />
            </div>

            <div class="flex flex-col mb-2">
              <label for="email" class="mb-1 text-sm text-at-light-green"
                >Have you accessed ILA (Independent Learning Accounts) from Skills Development
                Scotland this year</label
              >
              <input
                type="email"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.accessIla"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="email" class="mb-1 text-sm text-at-light-green"
                >Would you like help to access any other education including adult literacy and
                numeracy or English Language courses i.e. EAL and ESL, TEFL</label
              >
              <input
                type="email"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.accessEducation"
              />
            </div>

            <div class="flex flex-col mb-2">
              <label for="email" class="mb-1 text-sm text-at-light-green">Details</label>
              <input
                type="email"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.details"
              />
            </div>

            <button
              @click="recordEducation"
              type="button"
              class="mt-6 py-2 px-6 rounded-sm self-start text-sm text-white bg-at-light-green duration-200 border-solid border-2-transparent hover:border-at-light-green hover:bg-white hover:text-at-light-green"
            >
              Proceed
            </button>
          </div>
        </div>

        <hr />
        <!--Education and immigration needs consent-->
        <div class="flex flex-col mt-8 mb-8">
          <h1 class="text-3xl text-at-light-green mb-4">Immigration details</h1>
          <p class="text-2xl ">
            This section will be looking at your immigration needs. Would you be happy for us to ask
            you some questions about that . Would you be happy for us to ask you some questions
            about that
          </p>
          <p class="text-2xl text-at-light-green"></p>
          <select
            @change="immigrationChange"
            id="immigration-Choice"
            class="mx-auto mt-8 p-2 text-gray-500 focus:outline-none"
            required
            v-model="immigrationChoice"
          >
            <option value="educationChoice">Choose your choice</option>
            <option value="yes">Yes</option>
            <option value="no">No</option>
          </select>
        </div>

        <!-- Education and immigration needs -->
        <div v-if="immigrationChoice === 'yes'" class="max-w-screen px-4 py-10">
          <div class="gap-y-2 relative" v-for="(item, index) in immigrations" :key="index">
            <div class="flex flex-col mb-2">
              <label for="firstName" class="mb-1 text-sm text-at-light-green"
                >If you find that you need help in this area, would you be happy for us to try to
                connect you to the appropriate place</label
              >
              <input
                type="text"
                required
                class="p-2 w-full text-gray-500 focus:outline-none"
                v-model="item.needConnect"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="lastName" class="mb-1 text-sm text-at-light-green"
                >Do you have any immigration needs?</label
              >
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.immigrationNeeds"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="email" class="mb-1 text-sm text-at-light-green"
                >Can you briefly describe your immigration needs</label
              >
              <input
                type="email"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.needsDetails"
              />
            </div>

            <button
              @click="recordImmigration"
              type="button"
              class="mt-6 py-2 px-6 rounded-sm self-start text-sm text-white bg-at-light-green duration-200 border-solid border-2-transparent hover:border-at-light-green hover:bg-white hover:text-at-light-green"
            >
              Proceed
            </button>
          </div>
        </div>

        <!--Social and community needs consent-->
        <div class="flex flex-col">
          <h1 class="text-3xl text-at-light-green mb-4">Community details</h1>
          <p class="text-2xl ">
            This section will be looking at your community needs. Would you be happy for us to ask
            you some questions about that . Would you be happy for us to ask you some questions
            about that
          </p>
          <p class="text-2xl text-at-light-green"></p>
          <select
            @change="communityChange"
            id="community-Choice"
            class="mx-auto mt-8 p-2 text-gray-500 focus:outline-none"
            required
            v-model="communityChoice"
          >
            <option value="communityChoice">Choose your choice</option>
            <option value="yes">Yes</option>
            <option value="no">No</option>
          </select>
        </div>

        <!-- social and community needs -->
        <div v-if="communityChoice === 'yes'" class="max-w-screen px-4 py-10">
          <div class="gap-y-2 relative" v-for="(item, index) in communities" :key="index">
            <div class="flex flex-col mb-2">
              <label for="firstName" class="mb-1 text-sm text-at-light-green"
                >If you find that you need help in this area, would you be happy for us to try to
                connect you to the appropriate place</label
              >
              <input
                type="text"
                required
                class="p-2 w-full text-gray-500 focus:outline-none"
                v-model="item.needConnect"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="lastName" class="mb-1 text-sm text-at-light-green"
                >We have various events and activities running in our church would you be interested
                in?</label
              >
              <input
                type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.churchActivities"
              />
            </div>
            <div class="flex flex-col mb-2">
              <label for="email" class="mb-1 text-sm text-at-light-green"
                >Our Church supports people in HMP Grampian and those being released from prison to
                the community. Are you or any of your family in need of support within the criminal
                justice system</label
              >
              <input
                type="email"
                required
                class="p-2 text-gray-500 focus:outline-none"
                v-model="item.criminalSupport"
              />
            </div>

            <button
              @click="recordCommunity"
              type="button"
              class="mt-6 py-2 px-6 rounded-sm self-start text-sm text-white bg-at-light-green duration-200 border-solid border-2-transparent hover:border-at-light-green hover:bg-white hover:text-at-light-green"
            >
              Proceed
            </button>
          </div>
        </div>

        <button
          type="submit"
          class="mx-auto mt-16 py-2 px-6 rounded-sm self-start text-sm text-white bg-at-light-green duration-200 border-solid border-2-transparent hover:border-at-light-green hover:bg-white hover:text-at-light-green"
        >
          SUBMIT
        </button>
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
    const healthChoice = ref('health-choice')
    const spiritualChoice = ref('spiritual-choice')
    const practicalChoice = ref('practical-choice')
    const accomodationChoice = ref('accomodation-choice')
    const employmentChoice = ref('employment-choice')
    const educationChoice = ref('education-choice')
    const immigrationChoice = ref('immigration-choice')
    const communityChoice = ref('Choose your choice')
    const statusMsg = ref(null)
    const errorMsg = ref(null)
    const personals = ref([])
    const personalsRecorded = ref(false)
    const financialsRecorded = ref(false)
    const healthRecorded = ref(false)
    const spiritualRecorded = ref(false)
    const financials = ref([])
    const spirituals = ref([])
    const healths = ref([])
    const practicals = ref([])
    const accomodations = ref([])
    const employments = ref([])
    const educations = ref([])
    const immigrations = ref([])
    const communities = ref([])

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

    // check choice of finance choice and display financial details if yes
    const fillFinance = () => {
      if (financeChoice.value === 'yes') {
        financials.value.push({
          id: uid(),
          connectChoice: '',
          billsDifficulty: '',
          helpDetails: '',
          debtDifficulties: '',
          budgetUse: '',
          incomeSource: '',
          others: '',
          support: ''
        })
        return
      }
    }

    // check choice of finance choice and display health details if yes
    const fillHealth = () => {
      if (healthChoice.value === 'yes') {
        healths.value.push({
          id: uid(),
          docRegistration: '',
          dentistRegistration: '',
          accessHelp: '',
          healthRate: '',
          mentalHealth: '',
          sexualHealth: '',
          dentalHealth: '',
          dietDescription: '',
          engagingHelp: '',
          supportSource: '',
          accessingCare: '',
          areaHelp: ''
        })
        return
      }
    }

    // check choice of finance choice and display health details if yes
    const fillSpiritual = () => {
      if (spiritualChoice.value === 'yes') {
        spirituals.value.push({
          id: uid(),
          spiritualOrReligious: '',
          religiousBeliefs: '',
          beliefDetails: '',
          faithLevel: '',
          faithInvolvement: '',
          involvmentDetails: ''
        })
        return
      }
    }

    // check choice of practical choice and display practical details if yes
    const fillPractical = () => {
      if (practicalChoice.value === 'yes') {
        practicals.value.push({
          id: uid(),
          needConnect: '',
          supportArea: '',
          details: ''
        })
        return
      }
    }

    // check choice of accomodation choice and display accomodation details if yes
    const fillAccomodation = () => {
      if (accomodationChoice.value === 'yes') {
        accomodations.value.push({
          id: uid(),
          needConnect: '',
          accomodationChoice: '',
          accomodationSituation: '',
          details: ''
        })
        return
      }
    }

    // check choice of employment choice and display employment details if yes
    const fillEmployment = () => {
      if (employmentChoice.value === 'yes') {
        employments.value.push({
          id: uid(),
          needConnect: '',
          accomodationSituation: '',
          details: ''
        })
        return
      }
    }

    // check choice of education choice and display education details if yes
    const fillEducation = () => {
      if (educationChoice.value === 'yes') {
        educations.value.push({
          id: uid(),
          needConnect: '',
          accomodationSituation: '',
          details: ''
        })
        return
      }
    }

    // check choice of education choice and display education details if yes
    const fillImmigration = () => {
      if (immigrationChoice.value === 'yes') {
        immigrations.value.push({
          id: uid(),
          needConnect: '',
          immigrationNeeds: '',
          needsDetails: ''
        })
        return
      }
    }

    // check choice of community choice and display community details if yes
    const fillCommunity = () => {
      if (communityChoice.value === 'yes') {
        communities.value.push({
          id: uid(),
          needConnect: '',
          churchActivities: '',
          criminalSupport: ''
        })
        return
      }
    }

    // Listens for changes in the personal choice
    const choiceChange = () => {
      personals.value = []
      fillPersonal()
    }

    // Listens for change in finance choice
    const financeChange = () => {
      financials.value = []
      fillFinance()
    }

    // Listens for change in health choice
    const healthChange = () => {
      healths.value = []
      fillHealth()
    }

    // Listens for change in spiritual choice
    const spiritualChange = () => {
      spirituals.value = []
      fillSpiritual()
    }

    // Listens for change in practical choice
    const practicalChange = () => {
      practicals.value = []
      fillPractical()
    }

    // Listens for change in accomodation choice
    const accomodationChange = () => {
      accomodations.value = []
      fillAccomodation()
    }

    // Listens for change in employment choice
    const employmentChange = () => {
      employments.value = []
      fillEmployment()
    }

    // Listens for change in education choice
    const educationChange = () => {
      educations.value = []
      fillEducation()
    }

    // Listens for change in immigration choice
    const immigrationChange = () => {
      immigrations.value = []
      fillImmigration()
    }

    // Listens for change in community choice
    const communityChange = () => {
      communities.value = []
      fillCommunity()
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
        statusMsg.value = 'success: personal details submitted!'
        personals.value = []
        personalsRecorded.value = true
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
        const { error } = await supabase.from('financials').insert([
          {
            financials: financials.value
          }
        ])
        if (error) throw error
        statusMsg.value = 'success: financial details submitted!'
        financials.value = []
        financialsRecorded.value = true
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

    // Record the health details
    const recordHealth = async () => {
      try {
        const { error } = await supabase.from('healths').insert([
          {
            healths: healths.value
          }
        ])
        if (error) throw error
        statusMsg.value = 'success: financial details submitted!'
        personals.value = []
        healthRecorded.value = true
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

    // Record the spiritual details
    const recordSpiritual = async () => {
      try {
        const { error } = await supabase.from('spirituals').insert([
          {
            spirituals: spirituals.value
          }
        ])
        if (error) throw error
        statusMsg.value = 'success: spiritual details submitted!'
        personals.value = []
        spiritualRecorded.value = true
        setTimeout(() => {
          statusMsg.value = false
        }, 5000)
      } catch (error) {
        errorMsg.value = `Error:${error.message}`
        setTimeout(() => {
          errorMsg.value = false
        }, 10000)
      }
    }

    // Record the practical details
    const recordPractical = async () => {
      try {
        const { error } = await supabase.from('practicals').insert([
          {
            practicals: practicals.value
          }
        ])
        if (error) throw error
        statusMsg.value = 'success: practical details submitted!'
        practicals.value = []
        spiritualRecorded.value = true
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

    // Record the accomodation details
    const recordAccomodation = async () => {
      try {
        const { error } = await supabase.from('accomodations').insert([
          {
            accomodation: accomodations.value
          }
        ])
        if (error) throw error
        statusMsg.value = 'success: accomodation details submitted!'
        accomodations.value = []
        spiritualRecorded.value = true
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

    // Record the employment details
    const recordEmployment = async () => {
      try {
        const { error } = await supabase.from('employments').insert([
          {
            employment: employments.value
          }
        ])
        if (error) throw error
        statusMsg.value = 'success: employment details submitted!'
        employments.value = []
        spiritualRecorded.value = true
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
    // Record the education details
    const recordEducation = async () => {
      try {
        const { error } = await supabase.from('educations').insert([
          {
            education: educations.value
          }
        ])
        if (error) throw error
        statusMsg.value = 'success: education details submitted!'
        educations.value = []
        spiritualRecorded.value = true
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

    // Record the immigration details
    const recordImmigration = async () => {
      try {
        const { error } = await supabase.from('immigrations').insert([
          {
            immigrations: immigrations.value
          }
        ])
        if (error) throw error
        statusMsg.value = 'success: immigration details submitted!'
        immigrations.value = []
        spiritualRecorded.value = true
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

    // Record the immigration details
    const recordCommunity = async () => {
      try {
        const { error } = await supabase.from('communities').insert([
          {
            communities: communities.value
          }
        ])
        if (error) throw error
        statusMsg.value = 'success: Community details submitted!'
        communities.value = []
        spiritualRecorded.value = true
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

    const finish = () => {
      router.push({ name: 'Thanks' })
    }
    return {
      finish,
      errorMsg,
      consentChoice,
      personals,
      financials,
      healths,
      spirituals,
      practicals,
      employments,
      educations,
      immigrations,
      communities,
      financeChoice,
      healthChoice,
      spiritualChoice,
      practicalChoice,
      employmentChoice,
      educationChoice,
      accomodationChoice,
      immigrationChoice,
      communityChoice,
      statusMsg,
      personalsRecorded,
      financialsRecorded,
      healthRecorded,
      choiceChange,
      fillPersonal,
      recordPersonals,
      fillFinance,
      financeChange,
      recordFinancials,
      healthChange,
      practicalChange,
      fillHealth,
      recordHealth,
      fillSpiritual,
      fillPractical,
      fillEmployment,
      fillEducation,
      fillImmigration,
      spiritualChange,
      accomodationChange,
      employmentChange,
      educationChange,
      immigrationChange,
      communityChange,
      recordSpiritual,
      router,
      recordPractical,
      recordAccomodation,
      recordEmployment,
      recordEducation,
      recordImmigration,
      recordCommunity
    }
  }
}
</script>

<style scoped>
.status-message {
  width: 30%;
  min-height: 50px;
  border-radius: 5px;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  background-color: white; /* Customize the background color */
  color: white; /* Customize the text color */
  padding: 10px;
  text-align: center;
  z-index: 999; /* Ensure it's on top of other content */
}
.image-container{
  width: 20px;
  height: 20px;
  margin-top: 3px;
  margin-left: 5px;
}
</style>
