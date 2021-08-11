<template>
  <div class="card shadow">
    <img :src=" 'images/' + menu.gambar " class="card-img-top" />
    <div class="card-body">
      <h5 class="card-title">{{ menu.nama }}</h5>
      <h6 class="card-subtitle mb-2 text-muted">{{ menu.kategori }}</h6>
      <p class="card-text">
        Harga : Rp.{{ menu.harga }}
      </p>
      <router-link to="#" class="btn btn-success btn-block"><b-icon-cart></b-icon-cart> Pesan</router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardMenus",
  props: ["menu"],
};
</script>

<style>
</style>