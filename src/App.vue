<script>
export default {
  data() {
    return {
      api_key: "f17de3b9417d698b94664fb1fc28ae59",
      url_base: `https://api.openweathermap.org/data/2.5/`,
      query: "",
      search_url: ``,
      data: {},
    };
  },

  methods: {
    getData(e) {
      if (e.key == "Enter") {
        fetch(
          `${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`
        )
          .then((response) => response.json())
          .then((data) => (this.data = data));
      }
    },
    getDate(e) {
      if (e.key == "Enter") {
        let date = new Date();
        console.log(date);
      }
    },
  },
};
</script>

<template>
  <div class="main">
    <div class="container">
      <div class="searchBox">
        <input
          class="search"
          type="text"
          placeholder="Search..."
          v-model="query"
          @keypress="getData"
        />
      </div>
      <div v-if="typeof data.main != 'undefined'" class="content">
        <h1 class="local">{{ data.name }}, {{ data.sys.country }}</h1>
        <p class="temp">{{ data.main.temp }}°c</p>
        <p class="data">{{ data.weather[0].main }}</p>
      </div>
      <div v-else></div>
    </div>
  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.main {
  width: 100vw;
  height: 100vh;

  background-image: url(./assets/backImg.jpg);
}
.container {
  background-size: 100vw;
  background-color: rgba(114, 114, 114, 0.431);

  width: 100vw;
  height: 100vh;

  display: flex;
  align-items: center;
  flex-direction: column;
}

.searchBox .search {
  margin-top: 200px;
  padding-left: 10px;
  width: 400px;
  height: 50px;
  background: rgba(255, 255, 255, 0.397);

  display: flex;
  align-items: center;
  justify-content: center;

  transition: 0.4s;
  border-radius: 16px 0px;
  border: 0;
  outline: none;
}

.searchBox .search:focus {
  background: rgba(255, 255, 255, 0.731);

  border-radius: 0px 16px;
}
.content {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

.content h1 {
  padding: 20px 0px;
}

.temp {
  padding: 20px;
  background-color: rgba(255, 255, 255, 0.574);
  border-radius: 8px;
  font-size: 40px;
  color: #292929;
}

.data {
  margin-top: 25px;
  font-size: 40px;
}
</style>
