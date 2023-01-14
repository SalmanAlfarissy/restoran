<template>
  <div class="hero">
    <!-- dekstop -->
    <div class="d-none d-md-block">
        <div class="row mt-4">
            <div class="col-md-6">
              <div class="d-flex h-100">
                <div class="justify-content-center align-self-center">
                  <h2><strong>Delicious Food Menu,</strong><br />In Your Gadget</h2>
                  <p>Ayo sergera pilih dan pesan makanan favorit anda!!</p>
                  <router-link class="btn btn-lg btn-success" to="/foods">
                    <b-icon-arrow-right></b-icon-arrow-right> Pesan
                  </router-link>
                </div>
              </div>
            </div>
            <div class="col-md-6">
              <img src="../assets/images/hero.png" width="100%" />
            </div>
        </div>
    </div>

    <!-- mobile -->
    <div class="d-sm-block d-md-none">
        <div class="row mt-4">
          <div class="col-md-6 mb-3">
            <img src="../assets/images/hero.png" width="100%" />
          </div>
            <div class="col-md-6">
              <div class="d-flex h-100">
                <div class="justify-content-center align-self-center">
                  <h2><strong>Delicious Food Menu,</strong><br />In Your Gadget</h2>
                  <p>Ayo sergera pilih dan pesan makanan favorit anda!!</p>
                  <router-link class="btn btn-lg btn-success" to="/foods">
                    <b-icon-arrow-right></b-icon-arrow-right> Pesan
                  </router-link>
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

<style scoped>
</style>