<template>
  <div id="app">
    <ShowWeather />
    <h1 class="page-title">{{ title }}</h1>
    <AddTask />
  </div>
</template>

<script>
import AddTask from './components/AddTask'
import ShowWeather from './components/ShowWeather'



export default {
  name: 'App',
  components: {
    AddTask,
    ShowWeather,
  },
  data() {
    return {
        title: 'Daily Task List'
    }
  }
}
</script>

<style>
.page-title {
  display: flex;
  margin-top: 40px;
  justify-content: center;
}

#app {
  height: 100vh;
  background-color: #c7f8ff;
}

@media (max-width: 510px) {
  #app {
    width: 375px;
    height: 736px;
    background-color: #c7f8ff;
  }
}
</style>
