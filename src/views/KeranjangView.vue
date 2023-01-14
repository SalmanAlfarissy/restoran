<template>
  <div class="keranjang-view">
    <Navbar :updateKeranjang="keranjangs" />
    <div class="container">
      <div class="row mt-4">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item">
                <router-link class="text-dark" to="/">Home</router-link>
              </li>
              <li class="breadcrumb-item">
                <router-link class="text-dark" to="/foods">Foods</router-link>
              </li>
              <li class="breadcrumb-item active" aria-current="page">
                Keranjang
              </li>
            </ol>
          </nav>
        </div>
      </div>

      <div class="row">
        <div class="col">
          <h2>Keranjang <strong>Saya</strong></h2>
          <div class="table-responsive mt-3">
            <table class="table">
              <thead>
                <tr>
                  <th scope="col">#</th>
                  <th scope="col">Foto</th>
                  <th scope="col">Makanan</th>
                  <th scope="col">Keterangan</th>
                  <th scope="col">Jumlah</th>
                  <th scope="col">Harga</th>
                  <th scope="col">Total Harga</th>
                  <th scope="col">Hapus</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(item, index) in keranjangs" :key="item.id">
                  <th>{{ index + 1 }}</th>
                  <td>
                    <img
                      :src="require('@/assets/images/' + item.product.gambar)"
                      alt="..."
                      class="img-fluid shadow"
                      width="250"
                    />
                  </td>
                  <td>
                    <strong>{{ item.product.nama }}</strong>
                  </td>
                  <td>{{ item.keterangan ? item.keterangan : "-" }}</td>
                  <td>{{ item.jumlah_pemesanan }}</td>
                  <td align="right">Rp. {{ item.product.harga }},00</td>
                  <td align="right">
                    <strong
                      >Rp.
                      {{
                        item.jumlah_pemesanan * item.product.harga
                      }},00</strong
                    >
                  </td>
                  <td align="center" class="text-danger">
                    <b-icon-trash
                      @click="hapusKeranjang(item.id)"
                    ></b-icon-trash>
                  </td>
                </tr>
                <tr>
                  <td colspan="6" align="right"><strong>Total : </strong></td>
                  <td align="right">
                    <strong>Rp. {{ totalHarga }},00 </strong>
                  </td>
                  <td></td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>

      <!-- checkout -->
      <div class="row justify-content-end">
        <div class="col-md-4">
          <form class="mt-4" v-on:submit.prevent>
            <div class="form-group">
              <label for="nama">Nama : </label>
              <input type="text" class="form-control" v-model="pesan.nama" />
            </div>
            <div class="form-group">
              <label for="noMeja">Nomor Meja : </label>
              <input type="text" class="form-control" v-model="pesan.noMeja" />
            </div>

            <button
              type="submit"
              class="btn btn-success float-right"
              @click="checkout"
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
  name: "KeranjangView",
  components: {
    Navbar,
  },
  data() {
    return {
      keranjangs: [],
      pesan: {},
    };
  },
  methods: {
    setKeranjangs(data) {
      this.keranjangs = data;
    },
    checkout() {
      if (this.pesan.nama && this.pesan.noMeja) {
        this.pesan.keranjangs = this.keranjangs;
        axios
          .post("http://localhost:3000/pesanans", this.pesan)
          .then(() => {
            // Hapus Keranjangs
            this.keranjangs.map((item) => {
              return axios
                .delete("http://localhost:3000/keranjangs/" + item.id)
                .then(() => {
                  this.$router.push({
                    path: "/pesanan-sukses",
                  });
                })
                .catch((error) => {
                  console.log("Gagal : ", error);
                });
            });

            this.$toast.success("Success Di Pesan..", {
              type: "success",
              position: "top-right",
              duration: 3000,
              dismissible: true,
            });
          })
          .catch((err) => {
            console.log(err);
          });
      } else {
        this.$toast.error("Nama dan Nomor Meja Harus di isi..", {
          type: "error",
          position: "top-right",
          duration: 3000,
          dismissible: true,
        });
      }
    },
    hapusKeranjang(id) {
      axios
        .delete("http://localhost:3000/keranjangs/" + id)
        .then(() => {
          this.$toast.error("Sukses hapus keranjang..", {
            type: "error",
            position: "top-right",
            duration: 3000,
            dismissible: true,
          });

          //reload data keranjang
          axios
            .get("http://localhost:3000/keranjangs")
            .then((response) => {
              this.setKeranjangs(response.data);
            })
            .catch((error) => {
              console.log("Gagal : ", error);
            });
        })
        .catch((error) => {
          console.log("Gagal : ", error);
        });
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/keranjangs/")
      .then((response) => {
        this.setKeranjangs(response.data);
      })
      .catch((error) => {
        console.log("Gagal : ", error);
      });
  },
  computed: {
    totalHarga() {
      return this.keranjangs.reduce((items, data) => {
        return items + data.product.harga * data.jumlah_pemesanan;
      }, 0);
    },
  },
};
</script>

<style>
</style>