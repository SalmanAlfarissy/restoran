<template>
  <div class="pesanan-sukses">
    <Navbar />
    <div class="container">
        <div class="row jastify-content-center mt-5">
            <div class="col text-center">
                <img src="@/assets/images/menunggu.png" alt="..." width="300">
                <h2><strong>Sukses!!</strong></h2>
                <h4>Pesanan Anda Segera di Proses <br/> Selamat Menunggu!</h4>
            </div>
        </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
export default {
  name: "PesananSuksesView",
  components: {
    Navbar,
  },
};
</script>

<style scoped>
</style>