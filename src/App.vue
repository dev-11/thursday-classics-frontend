<template>
  <div id="app">
    <section v-if="errored">
      <p>We're sorry, we're not able to retrieve this information at the moment, please try back later</p>
    </section>
    <section v-else>
      <div v-if="loading">
        <div class="spinner-border text-primary" role="status">
          <span class="sr-only">Loading...</span>
        </div>
      </div>
      <div v-else>
        <div class="outer">
          <div v-bind:key="i" v-for="(movie, i) in movies">
            <Card v-bind:info="movie"/>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>

import axios from "axios";
import Card from "./components/Card.vue";

export default {
    name: "App",
    data() {
        return {
            movies: [],
            errored: false,
            loading: true
        };
    },
    created() {
        axios
            .get("https://api.masterbranch.io/b/tc")
            .then(response => (this.movies = response.data.body.data)
        )
            .catch(error => {
            console.log(error);
            this.errored = true;
        })
            .finally(() => (this.loading = false));
    },
    components: { Card }
};
</script>

<style>
body {
  display: flex;
  justify-content: center;
  background: #f6f6f6;
  font-family: "Roboto Slab", serif;
  line-height: 1.4;
}
.spinner-border {
  position: fixed;
  z-index: 1;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  width: 50px;
  height: 50px;
  margin: auto;
}
#app{
    width: 100%;
}
.outer {
  border: 1px solid #000;
  /* display:flex; */
  /* justify-content: center; */
  padding: 3px;
}
.outer > div {
  margin:2px;
}
</style>
