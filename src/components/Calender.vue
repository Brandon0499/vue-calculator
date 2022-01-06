<template>
  <div class="m-auto" style="width: 50%">
    <h1 class="text-2xl my-2 text-center">Vue Calender</h1>
    <section class="mx-4 flex justify-between">
      <h2 class="font-bold">{{ currentMonthName }}</h2>
      <h2 class="font-bold">{{ currentYear }}</h2>
    </section>

    <section class="flex my-2">
      <p
        class="text-center"
        style="width: 14.28%"
        v-for="(day, index) in days"
        :key="index"
      >
        {{ day }}
      </p>
    </section>
    <section class="flex flex-wrap h-48">
      <!-- the first p tag loops through the days that is supposed to leave blank-->
      <!-- the second p tag will start outputting the days number for that month -->
      <p
        class="text-center"
        style="width: 14.28%"
        v-for="num in startDay()"
        :key="num"
      ></p>
      <p
        class="text-center"
        style="width: 14.28%"
        v-for="num in daysInMonth()"
        :key="num"
        :class="{ colored: compareAll(num) }"
      >
        <!-- compoare each date and see whether the date is equals to todays date -->
        {{ num }}
      </p>
    </section>
    <section class="flex justify-between my-4">
      <button class="px-2 border rounded" @click="prev">Prev</button>
      <button class="px-2 border rounded" @click="next">Next</button>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentDate: new Date().getDate(),
      currentMonth: new Date().getMonth(),
      currentYear: new Date().getFullYear(),
      days: ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"],
    };
  },
  methods: {
    daysInMonth() {
      // const month = new Date().getMonth() + 1;
      return new Date(this.currentYear, this.currentMonth + 1, 0).getDate();
    },
    startDay() {
      // this gets the first day of the current month
      return new Date(this.currentYear, this.currentMonth, 1).getDay();
    },
    next() {
      if (this.currentMonth === 11) {
        this.currentMonth = 0;
        this.currentYear++;
      } else {
        this.currentMonth++;
      }
    },
    prev() {
      if (this.currentMonth === 0) {
        // set it back to december
        this.currentMonth = 11;
        this.currentYear--;
      } else {
        this.currentMonth--;
      }
    },
    compareAll(num) {
      // toDateString() returns only the date portion of the date without the time
      let result =
        new Date(this.currentYear, this.currentMonth, num).toDateString() ===
        new Date().toDateString();
      return result;
    },
  },
  computed: {
    currentMonthName() {
      return new Date(this.currentYear, this.currentMonth).toLocaleString(
        "default",
        {
          month: "long",
        }
      );
    },
  },
};
</script>

<style>
.colored {
  color: red;
}
</style>
