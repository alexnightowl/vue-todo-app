<template>
  <div class="calendar">
    <v-date-picker
      mode="single"
      tint-color="#f142f4"
      v-model="selectedDate"
      :theme-styles="themeStyles"
      is-double-paned
      is-inline
      @dayclick="selectDate"
    >
    </v-date-picker>
  </div>
</template>

<script>
export default {
  name: "calendar",
  data() {
    return {
      selectedDate: new Date(),
      themeStyles: {
        wrapper: {
          border: "1",

        },
        header: {
          color: "#fafafa",
          backgroundColor: "#f142f4",
          borderColor: "#404c59",
          borderWidth: "1px 1px 0 1px",
        },
        headerVerticalDivider: {
          borderLeft: "1px solid #404c59",
        },
        weekdays: {
          color: "#ffffff",
          backgroundColor: "#f142f4",
          borderColor: "#ff0098",
          borderWidth: "0 1px",
          padding: "5px 0 10px 0",
        },
        weekdaysVerticalDivider: {
          borderLeft: "1px solid #404c59",
        },
        weeks: {
          border: "1px solid #dadada",
        },
      },
    };
  },
  computed: {
    filteredTodosByDate() {
      if (this.selectedDate) {
        return `${this.selectedDate.getDate()}/${this.selectedDate.getMonth()+1}/${this.selectedDate.getFullYear()}`;
      } else return "without date";
    },
  },
  methods: {
    selectDate() {
      this.$emit('add-date', this.filteredTodosByDate);
    },
  },
};
</script>
<style>
.calendar {
  margin-right: 1rem;
}
</style>