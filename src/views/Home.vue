<template>
  <div class="home">
    <Navbar />
    <div class="container">
      <Hero />
      <div class="row mt-4">
        <div class="col">
          <h2>Favorites <strong>Menus</strong></h2>
        </div>
        <div class="col">
          <router-link to="/menu" class="btn btn-success float-right"><b-icon-eye></b-icon-eye> Lihat Semua</router-link>
        </div>
      </div>

      <div class="row mb-3">
        <div class="col-md-3 mt-4" v-for="menu in menus" :key="menu.id">
          <CardMenus :menu="menu" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from "@/components/Navbar.vue";
import Hero from "@/components/Hero.vue";
import CardMenus from "@/components/CardMenus.vue";
import axios from "axios";

export default {
  name: "Home",
  components: {
    Navbar,
    Hero,
    CardMenus,
  },
  data() {
    return {
      menus: [],
    };
  },
  methods: {
    setMenus(data) {
      this.menus = data;
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/favorite-menus")
      .then((response) => this.setMenus(response.data))
      .catch((error) => console.log(error));
  },
};
</script>
