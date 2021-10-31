<template>
  <div class="cart">
    <Navbar :updateCart="pesanan"/>
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
                  <th scope="col"></th>
                  <th scope="col">#</th>
                  <th scope="col">Menu</th>
                  <th scope="col">Description</th>
                  <th scope="col">Qty</th>
                  <th scope="col">Price</th>
                  <th scope="col">Sub Total</th>
                  <th scope="col">Action</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(pesanan,index) in pesanan" :key="pesanan.id">
                  <td>{{index+1}}</td>
                  <td>
                    <img :src="'../images/' + pesanan.menu.gambar" class="img-fluid shadow" style="max-height:100px">
                  </td>
                  <td><strong>{{pesanan.menu.nama}}</strong></td>
                  <td>{{pesanan.keterangan ? pesanan.keterangan : "-"}}</td>
                  <td>{{pesanan.jumlah_pesanan}}</td>
                  <td align="right">Rp. {{pesanan.menu.harga.toLocaleString()}}</td>
                  <td align="right"><strong>Rp. {{(pesanan.jumlah_pesanan*pesanan.menu.harga).toLocaleString()}}</strong></td>
                  <td class="text-danger"><b-icon-trash @click="hapusKeranjang(pesanan.id)"></b-icon-trash></td>
                </tr>

                <tr>
                  <td colspan="6" align="right">
                    <strong>Total Price</strong>
                  </td>
                  <td align="right"><strong>Rp. {{totalHarga.toLocaleString()}}</strong></td>
                  <td></td>
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
    },
    hapusKeranjang(id){
      axios
      .delete("http://localhost:3000/carts/"+id)
      .then(() => {
        this.$toast.error("Berhasil hapus pesanan.", {
          type: "error",
          position: "top-right",
          duration: 3000,
          dismissible: true,
        });

        axios
        .get("http://localhost:3000/carts")
        .then((response) => this.setPesanan(response.data))
        .catch((error) => console.log(error));
      })
      .catch((error) => console.log(error));
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