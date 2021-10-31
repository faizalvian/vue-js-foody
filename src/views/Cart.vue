<template>
  <div class="cart">
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
                Order
              </li>
            </ol>
          </nav>
        </div>
      </div>

      <div class="row mt-3">
        <div class="col">
          <h2>Summary <strong>Orders</strong></h2>
          <div class="table-responsive">
            <table class="table">
              <thead>
                <tr>
                  <th scope="col">Menu</th>
                  <th scope="col">Description</th>
                  <th scope="col">Qty</th>
                  <th scope="col">Price</th>
                  <th scope="col">Sub Total</th>
                  <th scope="col">Action</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="pesanan in pesanan" :key="pesanan.id">
                  <td><strong>{{pesanan.menu.nama}}</strong></td>
                  <td>{{pesanan.keterangan}}</td>
                  <td>{{pesanan.jumlah_pesanan}}</td>
                  <td>Rp. {{pesanan.menu.harga}}</td>
                  <td><strong>Rp. {{pesanan.jumlah_pesanan*pesanan.menu.harga}}</strong></td>
                  <td class="text-danger"><b-icon-trash></b-icon-trash></td>
                </tr>

                <tr>
                  <td colspan="4" align="center">
                    <strong>Total Price</strong>
                  </td>
                  <td><strong>Rp. {{totalHarga}}</strong></td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import axios from "axios";
export default {
  name: "Cart",
  components: {
    Navbar,
  },
  data(){
    return {
      pesanan: []
    }
  },
  methods: {
    setPesanan(data){
      this.pesanan = data;
    }
  },
  mounted() {
    axios
      .get("http://localhost:3000/carts")
      .then((response) => this.setPesanan(response.data))
      .catch((error) => console.log(error));
  },
  computed: {
    totalHarga(){
      return this.pesanan.reduce(function(items, data){
        return items+(data.menu.harga*data.jumlah_pesanan)
      }, 0);
    }
  }
};
</script>

<style>
</style>