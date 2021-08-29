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
          <img
            :src="'../images/' + menu.gambar"
            class="img-fluid shadow img-detail"
          />
        </div>
        <div class="col-md-6">
          <h2>
            <strong>{{ menu.nama }}</strong>
          </h2>
          <p>{{ menu.kategori }}</p>
          <hr />
          <h4>Harga : {{ menu.harga }}</h4>
          <form v-on:submit.prevent>
            <div class="form-group">
              <label>Jumlah</label>
              <input
                type="number"
                class="form-control"
                v-model="pesan.jumlah_pesanan"
              />
            </div>
            <div class="form-group">
              <label>Keterangan</label>
              <textarea
                v-model="pesan.keterangan"
                class="form-control"
                rows="3"
                placeholder="Jangan pedes ya.."
              ></textarea>
            </div>
            <button
              type="submit"
              class="btn btn-success btn-block"
              @click="pemesanan"
            >
              <b-icon-cart></b-icon-cart> Pesan
            </button>
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
      pesan: {},
    };
  },
  methods: {
    setMenu(data) {
      this.menu = data;
    },
    pemesanan() {
      if (this.pesan.jumlah_pesanan) {
        this.$router.push({ path: "/cart" })
        this.pesan.menu = this.menu;
        axios
          .post("http://localhost:3000/carts", this.pesan)
          .then(() => {
            this.$toast.success("Berhasil masuk keranjang.", {
              type: "success",
              position: "top-right",
              duration: 3000,
              dismissible: true,
            });
          })
          .catch((err) => console.log(err));
      } else {
        this.$toast.success("Jumlah pesanan Anda masih kosong.", {
          type: "error",
          position: "top-right",
          duration: 3000,
          dismissible: true,
        });
      }
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