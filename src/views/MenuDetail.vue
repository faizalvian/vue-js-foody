<template>
  <div class="menu-detail">
    <Navbar />
    <div class="container">
      <div class="row mt-5">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item">
                <router-link class="text-dark" to="/">Home</router-link>
              </li>
              <li class="breadcrumb-item">
                <router-link class="text-dark" to="/menu">Menu</router-link>
              </li>
              <li class="breadcrumb-item active" aria-current="page">
                {{ menu.nama }}
              </li>
            </ol>
          </nav>
        </div>
      </div>
      <div class="row">
        <div class="col-md-6">
          <img :src="'../images/' + menu.gambar" class="img-fluid shadow img-detail" />
        </div>
        <div class="col-md-6">
          <h2>
            <strong>{{ menu.nama }}</strong>
          </h2>
          <p>{{ menu.kategori }}</p>
          <hr />
          <h4>Harga : {{ menu.harga }}</h4>
          <form>
            <div class="form-group">
              <label>Jumlah</label>
              <input type="number" class="form-control" />
            </div>
            <div class="form-group">
              <label>Keterangan</label>
              <textarea
                class="form-control"
                rows="3"
                placeholder="Jangan pedes ya.."
              ></textarea>
            </div>
            <router-link to="#" type="submit" class="btn btn-success btn-block"><b-icon-cart></b-icon-cart> Pesan</router-link>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import axios from "axios";

export default {
  name: "MenuDetail",
  components: {
    Navbar,
  },
  data() {
    return {
      menu: {},
    };
  },
  methods: {
    setMenu(data) {
      this.menu = data;
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/menus/" + this.$route.params.id)
      .then((response) => this.setMenu(response.data))
      .catch((error) => console.log(error));
  },
};
</script>

<style>
</style>