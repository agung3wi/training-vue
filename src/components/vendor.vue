<template>
  <div>
    <input v-model="nama" type="text" name="" id="a" placeholder="nama" />
    <input v-model="alamat" type="text" name="" id="b" placeholder="alamat" />
    <input v-model="email" type="text" name="" id="c" placeholder="email" />
    <button type="button" @click="submitVendor()">Tambah Vendor</button>
    <br />
    <pre>{{ vendor }}</pre>
    <table class="table table-striped table-inverse table-responsive">
      <thead class="thead-inverse">
        <tr>
          <th>Nama</th>
          <th>Alamat</th>
          <th>Email</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(v, index) in vendor" :key="index">
          <td>{{ v.vendor_name }}</td>
          <td>{{ v.vendor_address }}</td>
          <td>{{ v.email }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
export default {
  name: "table",
  data() {
    return {
      alamat: "",
      nama: "Adinda Yahya Hexatama",
      email: "",
      vendor: [],
    };
  },
  created() {
    // 2
    this.getVendor();
  },
  beforeMount() {
    // 3
    console.log("before-mount", this.nama);
  },
  mounted() {
    // 4
    this.vendor.push({
      nama: "nama-mounted",
      alamat: "alamat-mounted",
      email: "email-mounted",
    });
  },

  methods: {
    submitVendor() {
      let input = {
        vendor_name: this.nama,
        vendor_address: this.alamat,
        email: this.email,
      };
      this.$http
        .post("http://localhost:8000/vendor/create", input)
        .then((response) => {
          alert("Sukses");
          this.getVendor();
        })
        .catch((err) => {
          alert("Error");
        });
    },
    getVendor() {
      this.$http
        .get("http://localhost:8000/vendor")
        .then((response) => {
          this.vendor = response.data;
        })
        .catch((err) => {
          alert("Error");
        });
    },
  },
};
</script>
