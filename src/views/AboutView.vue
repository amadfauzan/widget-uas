<template>
  <div class="app">
    <div class="menu">
      <button @click="activeTab = 'about'">About</button>
      <button @click="activeTab = 'weather'">Weather</button>
      <button @click="activeTab = 'stopwatch'">Stopwatch</button>
      <button @click="activeTab = 'calendar'">Calendar</button>
      <button @click="activeTab = 'medications'">Medications</button>
      <button @click="activeTab = 'game'">Game</button>
    </div>

    <div class="content">
      <AboutPage v-show="activeTab === 'about'"></AboutPage>
      <WeatherWidget v-show="activeTab === 'weather'"></WeatherWidget>
      <StopwatchWidget v-show="activeTab === 'stopwatch'"></StopwatchWidget>
      <CalendarWidget v-show="activeTab === 'calendar'"></CalendarWidget>
      <MedicationsWidget v-show="activeTab === 'medications'"></MedicationsWidget>
      <GameWidget v-show="activeTab === 'game'"></GameWidget>
    </div>
  </div>
</template>

<script>
import AboutPage from '@/components/AboutPage.vue';
import WeatherWidget from '@/components/WeatherWidget.vue';
import StopwatchWidget from '@/components/StopwatchWidget.vue';
import CalendarWidget from '@/components/CalendarWidget.vue';
import MedicationsWidget from '@/components/MedicationsWidget.vue';
import GameWidget from '@/components/GameWidget.vue';

export default {
  name: 'App',
  components: {
    AboutPage,
    WeatherWidget,
    StopwatchWidget,
    CalendarWidget,
    MedicationsWidget,
    GameWidget
  },
  data() {
    return {
      activeTab: 'about'
    };
  }
};
</script>

<style>
.app {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

.menu {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

.menu button {
  margin-right: 10px;
  font-size: 1em;
  padding: 5px 10px;
  background-color: #000000;
  border: none;
  cursor: pointer;
}

.menu button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.menu button:hover {
  background-color: #6fa39c;
}

.content {
  border: 1px solid #ccc;
  padding: 20px;
}
</style>
