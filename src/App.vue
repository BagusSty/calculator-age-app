<script>
export default {
  name: "AgeCalc",
  data() {
    return {
      dateResult: false,
      pastYear: true,
      validDay: true,
      validMonth: true,
      emptyInput: false,
      years: 0,
      months: 0,
      days: 0,
      day: null,
      month: null,
      year: null,
    };
  },
  methods: {
    calculateAge() {
      const day = this.day;
      const month = this.month;
      const year = this.year;

      const date = new Date();
      const currentYear = date.getFullYear();
      const currentMonth = date.getMonth() + 1;
      const currentDay = date.getDate();

      let years = 0;
      if (
        currentMonth > month ||
        (currentMonth == month && currentDay >= day)
      ) {
        years = currentYear - year;
      } else {
        years = currentYear - year - 1;
      }

      let months = 0;
      if (currentDay >= day) {
        months = currentMonth - month;
      } else if (currentDay < day) {
        months = currentMonth - month - 1;
      }

      months = months < 0 ? months + 12 : months;

      let days = 0;
      let monthDays = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31];

      if ((year % 4 == 0 && year % 100 != 0) || year % 400 == 0) {
        monthDays[1] = 29;
      }

      if (currentDay >= day) {
        days = currentDay - day;
      } else if (currentDay < day) {
        days = currentDay - day + monthDays[month - 1];
      }

      if (day > monthDays[month - 1]) {
        this.validDay = false;
        this.dateResult = false;
      } else {
        this.validDay = true;
      }

      if (month > 12) {
        this.validMonth = false;
        this.dateResult = false;
      } else {
        this.validMonth = true;
      }

      if (years < 0) {
        this.dateResult = false;
        this.pastYear = false;
      } else if (day === null || month === null || year === null) {
        this.dateResult = false;
        this.emptyInput = true;
      } else if (
        this.validDay == false ||
        this.validMonth == false ||
        this.validYear == false
      ) {
        this.dateResult = false;
      } else {
        this.dateResult = true;
        this.pastYear = true;
        this.emptyInput = false;
        this.years = years;
        this.months = months;
        this.days = days;
      }
    },
  },
};
</script>
<template>
  <main class="app">
    <div class="flex justify-center items-center h-screen">
      <div
        class="max-w-2xl w-80 sm:w-full mx-auto m-4 bg-white shadow-lg rounded-t-2xl rounded-bl-2xl custom-rounded-br sm:p-12 p-8 text-center justify-center items-center"
      >
        <div class="flex">
          <div class="m-2">
            <label
              for="day"
              class="block text-left font-bold mb-2 text-lightGrey"
              :class="{ 'text-red-300': !validDay || emptyInput }"
              >DAY</label
            >
            <input
              class="text-semibold placeholder:text-lightGrey sm:p-3 p-2 sm:w-40 w-full border-lightGrey border cursor-pointer rounded-md hover:border-customPurple remove-arrow"
              :class="{ 'border-red-500': !validDay || emptyInput }"
              type="number"
              v-model="day"
              placeholder="DD"
              id="day"
              name="day"
              required:true
            />
            <hr />
            <span class="error italic text-red-500 font-thin" v-if="emptyInput"
              >This field is required</span
            >
            <span
              class="error italic text-red-500 font-thin"
              v-else-if="!validDay"
              >Must be a valid date</span
            >
          </div>
          <div class="m-2">
            <label
              for="day"
              class="block text-left font-bold mb-2 text-lightGrey"
              :class="{ 'text-red-300': !validMonth || emptyInput }"
              >MONTH</label
            >
            <input
              class="text-semibold placeholder:text-lightGrey sm:p-3 p-2 sm:w-40 w-full border-lightGrey border cursor-pointer rounded-md hover:border-customPurple remove-arrow"
              :class="{ 'border-red-500': !validMonth || emptyInput }"
              type="number"
              v-model="month"
              placeholder="MM"
              id="month"
              name="month"
              required:true
            />
            <hr />
            <span class="error italic text-red-500 font-thin" v-if="emptyInput"
              >This field is required</span
            >
            <span
              class="error italic text-red-500 font-thin"
              v-else-if="!validMonth"
              >Must be a valid month</span
            >
          </div>
          <div class="m-2">
            <label
              for="day"
              class="block text-left font-bold mb-2 text-lightGrey"
              :class="{ 'text-red-300': !pastYear || emptyInput }"
              >YEAR</label
            >
            <input
              class="text-semibold placeholder:text-lightGrey sm:p-3 p-2 sm:w-40 w-full border-lightGrey border cursor-pointer rounded-md hover:border-customPurple remove-arrow"
              :class="{ 'border-red-500': !pastYear || emptyInput }"
              type="number"
              v-model="year"
              placeholder="YYYY"
              id="year"
              name="year"
              required:true
            />
            <hr />
            <span class="error italic text-red-500 font-thin" v-if="emptyInput"
              >This field is required</span
            >
            <span
              class="error italic text-red-500 font-thin"
              v-else-if="!pastYear"
              >Must be a valid year</span
            >
          </div>
        </div>
        <div class="flex items-center justify-center">
          <hr class="border-t border-gray-300 flex-grow" />
          <button
            class="bg-customPurple p-2 rounded-full hover:bg-offBlack"
            @click="calculateAge()"
          >
            <img src="/assets/images/icon-arrow.svg" alt="" />
          </button>
        </div>
        <div class="mt-3 sm:text-7xl text-5xl">
          <div class="flex m-auto">
            <h1 class="text-customPurple font-bold mr-3" v-if="!dateResult">
              --
            </h1>
            <h1 class="text-customPurple font-bold mr-3" v-else>{{ years }}</h1>
            <h1 class="text-offBlack font-bold italic">years</h1>
          </div>
          <div class="flex m-auto">
            <h1 class="text-customPurple font-bold mr-3" v-if="!dateResult">
              --
            </h1>
            <h1 class="text-customPurple font-bold mr-3" v-else>{{ month }}</h1>
            <h1 class="text-offBlack font-bold italic">months</h1>
          </div>
          <div class="flex m-auto">
            <h1 class="text-customPurple font-bold mr-3" v-if="!dateResult">
              --
            </h1>
            <h1 class="text-customPurple font-bold mr-3" v-else>{{ days }}</h1>
            <h1 class="text-offBlack font-bold italic">days</h1>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
.custom-rounded-br {
  border-bottom-right-radius: 4rem;
}
.remove-arrow::-webkit-inner-spin-button,
.remove-arrow::-webkit-outer-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
</style>
