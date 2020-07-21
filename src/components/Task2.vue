<template>
  <v-container>
    <v-text-field
      label="Salary ($)"
      v-model="salary.wage"
      type="number"
    ></v-text-field>
    <v-select
      :items="timeScaleOptions"
      v-model="salary.timeScale"
      label="Salary Scale"
      dense
    ></v-select>
    <v-text-field
      label="Hours per Week"
      v-model="salary.hoursPerWeek"
      type="number"
    ></v-text-field>
    <v-text-field
      label="Days per Week"
      v-model="salary.daysPerWeek"
      type="number"
    ></v-text-field>
    <v-text-field
      label="Vacation days per Year"
      v-model="salary.vacationsPerYear"
      type="number"
    ></v-text-field>
    <v-text-field
      label="Holidays per year"
      v-model="salary.holidaysPerYear"
      type="number"
    ></v-text-field>
    <v-btn @click="calculateWage()" pb-4>Calculate Yearly Income</v-btn>

    <v-card v-if="wageCalculated" ma-4>
      <v-card-title>Your yearly wage</v-card-title>
      <v-card-subtitle
        >Based on the assumption that you get paid double for holidays and you
        work all of them.</v-card-subtitle
      >
      <v-card-text
        >${{ formatDollars(yearlyWage) }} is your calculated yearly
        wage</v-card-text
      >
    </v-card>
  </v-container>
</template>

<script>
export default {
  name: "Task2",

  data: () => ({
    salary: {
      wage: 30,
      timeScale: "hourly",
      hoursPerWeek: 40,
      daysPerWeek: 5,
      vacationsPerYear: 10,
      holidaysPerYear: 10,
    },
    timeScaleOptions: ["hourly", "weekly", "monthly", "Annual"],
    yearlyWage: null,
    wageCalculated: false,
    MONTHS_PER_YEAR: 12,
    WEEKS_PER_YEAR: 52.1428571,
  }),
  created() {},
  methods: {
    calculateWage() {
      // Vacation days are assumed to be paid
      let tempYearlyWage = 0;
      if (this.salary.timeScale == "hourly") {
        tempYearlyWage =
          this.salary.wage * this.salary.hoursPerWeek * this.WEEKS_PER_YEAR;
      } else if (this.salary.timeScale == "weekly") {
        tempYearlyWage = this.salary.wage * this.WEEKS_PER_YEAR;
      } else if (this.salary.timeScale == "monthly") {
        tempYearlyWage = this.salary.wage * this.MONTHS_PER_YEAR;
      } else {
        tempYearlyWage = this.salary.wage;
      }
      let workDaysPerYear = this.salary.daysPerWeek * this.WEEKS_PER_YEAR;
      // holidays are assumed to be paid at double rate
      let holidayBonus =
        (tempYearlyWage / workDaysPerYear) * this.salary.holidaysPerYear;
      this.yearlyWage = Number(tempYearlyWage) + Number(holidayBonus);
      this.wageCalculated = true;
    },
    formatDollars(value) {
      let val = (value / 1).toFixed(2).replace(".", ".");
      return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    },
  },
};
</script>
