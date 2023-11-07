<script>
export default {
  data() {
    return {
      inputs: [
        {
          label: "DAY",
          placeholder: "DD",
          vModel: "day",
        },
        {
          label: "MONTH",
          placeholder: "MM",
          vModel: "month",
        },
        {
          label: "YEAR",
          placeholder: "YYYY",
          vModel: "year",
        },
      ],
      age: [
        {
          text: "years",
        },
        {
          text: "months",
        },
        {
          text: "days",
        },
      ],
      results: [
        {
          day: "",
          month: "",
          year: "",
        },
      ],
    };
  },
  methods: {
    toggleAnswer(index) {
      this.faqs[index].showAnswer = !this.faqs[index].showAnswer;
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
          <div class="m-2" v-for="(input, index) in inputs" :key="index">
            <label
              for="day"
              class="block text-left font-bold mb-2 text-lightGrey"
              >{{ input.label }}</label
            >
            <input
              class="text-semibold placeholder:text-lightGrey sm:p-3 p-2 sm:w-40 w-full border-lightGrey border cursor-pointer rounded-md hover:border-customPurple remove-arrow"
              type="number"
              v-model="input.vModel"
              :placeholder="input.placeholder"
              :id="input.label"
              :name="input.label"
            />
          </div>
        </div>
        <div class="flex items-center justify-center">
          <hr class="border-t border-gray-300 flex-grow" />
          <button class="bg-customPurple p-2 rounded-full hover:bg-offBlack">
            <img src="/assets/images/icon-arrow.svg" alt="" />
          </button>
        </div>
        <div class="mt-3 sm:text-7xl text-5xl">
          <div class="flex m-auto" v-for="(ages, index) in age" :key="index">
            <h1 class="text-customPurple font-bold">--</h1>
            <h1 class="text-offBlack font-bold italic">{{ ages.text }}</h1>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script setup></script>

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
