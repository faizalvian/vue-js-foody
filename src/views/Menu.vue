<template>
  <div>
    <Navbar />
    <div class="container">
      <div class="row mt-4">
        <div class="col">
          <h2>Daftar <strong>Menu</strong></h2>
        </div>
        <div class="col">
          <div class="input-group mb-3">
            <input
              v-model="search"
              type="text"
              class="form-control"
              placeholder="Cari Makanan/minuman..."
              @keyup="searchMenu"
            />
            <div class="input-group-prepend">
              <span class="input-group-text" id="basic-addon1"
                ><b-icon-search></b-icon-search
              ></span>
            </div>
          </div>
        </div>
      </div>

      <div class="row mb-4">
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
import CardMenus from "@/components/CardMenus.vue";
import axios from "axios";

export default {
  name: "Menu",
  components: {
    Navbar,
    CardMenus,
  },
  data() {
    return {
      menus: [],
      search: "",
    };
  },
  methods: {
    setMenus(data) {
      this.menus = data;
    },
    searchMenu() {
      axios
        .get("http://localhost:3000/menus?q=" + this.search)
        .then((response) => this.setMenus(response.data))
        .catch((error) => console.log(error));
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/menus")
      .then((response) => this.setMenus(response.data))
      .catch((error) => console.log(error));
  },
};
</script>

<style></style>
