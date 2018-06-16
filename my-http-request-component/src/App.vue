<template>
  <div id="app">
    <ul v-if="data">
      <li v-for="item in data.items" :key="item.id">
        <h4>
          <a v-bind:href="item.html_url">{{item.name}}</a>
          <sub>star:{{item.stargazers_count}}, fork:{{item.forks_count}}</sub>
        </h4>
        <small>{{item.description}}</small>
      </li>
    </ul>
    <div v-else>
      数据加载中...
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "app",
  data: () => ({
    data: undefined
  }),
  mounted() {
    this.init();
  },
  methods: {
    init: function() {
      axios
        .get(
          "https://api.github.com/search/repositories?q=javascript&sort=stars&order=desc"
        )
        .then(response => (this.data = response.data))
        .catch(err => console.log(err));
    }
  }
};
</script>