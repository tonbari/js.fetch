<template>
  <div id="app">
    <h2>Список пользователей</h2>

    <div v-if="!isDataLoaded" class="preloader">... Идет загрузка ...</div>

    <div v-else v-for="user in users" :key="user.login.uuid">
      <img :src="user.picture.medium" alt="" />
      <br />
      <b>{{ user.name.first + ' ' + user.name.last }}</b>
      <div>{{ user.gender }}</div>
      <div>{{ user.email }}</div>
      <div>
        Улица {{ user.location.street.name + ' Город ' + user.location.city }}
      </div>
      <div>Возраст {{ user.dob.age }}</div>
      <div>{{ user.cell }}</div>
      <br />
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  components: {},

  data: function () {
    return {
      users: [],
      isDataLoaded: false,
    };
  },

  mounted: function () {
    fetch('https://randomuser.me/api/?results=10')
      .then((data) => data.json())
      .then((data) => {
        console.log(data);
        this.users = data.results;
        this.isDataLoaded = true;
      });
  },
};
</script>

<style>
#app {
  font-family: system-ui;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #808080;
  margin-top: 30px;
}

.preloader {
  color: red;
}

h2 {
  color: black;
}

b {
  color: #696969;
}
</style>
