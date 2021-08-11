<template>
  <div class="hero">
    <!-- Desktop -->
    <div class="d-none d-md-block">
      <div class="row mt-4">
        <div class="col-md-6">
          <div class="d-flex h-100">
            <div class="justify-content-center align-self-center">
              <h2>
                <strong>Our Delicious Foods, </strong><br />
                For Your Life
              </h2>
              <p>Nikmati kemudahan pesan makanan dalam satu aplikasi.</p>
              <button class="btn btn-success">
                <b-icon-arrow-right></b-icon-arrow-right> Pesan Sekarang
              </button>
            </div>
          </div>
        </div>
        <div class="col-md-6">
          <img src="../assets/images/hero.png" width="100%" />
        </div>
      </div>
    </div>

    <!-- Mobile -->
    <div class="d-sm-block d-md-none">
      <div class="row mt-4">
        <div class="col-md-6">
          <img src="../assets/images/hero.png" width="100%" />
        </div>
        <div class="col-md-6">
          <div class="d-flex h-100">
            <div class="justify-content-center align-self-center">
              <h2>
                <strong>Our Delicious Foods, </strong><br />
                For Your Life
              </h2>
              <p>Nikmati kemudahan pesan makanan dalam satu aplikasi.</p>
              <button class="btn btn-success">
                <b-icon-arrow-right></b-icon-arrow-right> Pesan Sekarang
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Hero",
};
</script>

<style>
</style>