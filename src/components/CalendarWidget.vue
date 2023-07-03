<template>
    <div class="calendar-widget">
      <h2>Calendar Widget</h2>
      <div v-if="isLoading">
        Loading calendar data...
      </div>
      <div v-else>
        <table>
          <thead>
            <tr>
              <th v-for="day in daysOfWeek" :key="day">{{ day }}</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="week in weeks" :key="week">
              <td v-for="day in week" :key="day" @click="selectDate(day)">
                <div class="date" :class="{ 'selected': selectedDate === day }">
                  {{ day }}
                </div>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'CalendarWidget',
    data() {
      return {
        isLoading: true,
        daysOfWeek: ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'],
        weeks: [],
        selectedDate: null
      };
    },
    mounted() {
      // Simulating an API call to fetch calendar data
      setTimeout(() => {
        this.isLoading = false;
        this.weeks = [
          [null, null, null, null, null, 1, 2],
          [3, 4, 5, 6, 7, 8, 9],
          [10, 11, 12, 13, 14, 15, 16],
          [17, 18, 19, 20, 21, 22, 23],
          [24, 25, 26, 27, 28, 29, 30]
        ];
      }, 2000);
    },
    methods: {
      selectDate(date) {
        this.selectedDate = date;
      }
    }
  };
  </script>
  
  <style scoped>
  .calendar-widget {
    border: 1px solid #ccc;
    padding: 20px;
    margin-bottom: 20px;
  }
  
  .calendar-widget h2 {
    margin-bottom: 10px;
  }
  
  .calendar-widget table {
    width: 100%;
    border-collapse: collapse;
  }
  
  .calendar-widget th,
  .calendar-widget td {
    border: 1px solid #ccc;
    padding: 10px;
    text-align: center;
  }
  
  .calendar-widget th {
    background-color: #f0f0f0;
  }
  
  .calendar-widget .date {
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  .calendar-widget .date.selected {
    background-color: #ffffff;
  }
  </style>
  