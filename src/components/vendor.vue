<template>
  <div>
    <input v-model="nama" type="text" name="" id="a" placeholder="nama">
    <input v-model="alamat" type="text" name="" id="b" placeholder="alamat">
    <input v-model="email" type="text" name="" id="c" placeholder="email">
    <button type="button" @click="submitVendor(nama)">Tambah Vendor</button>
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
        <tr v-for="(v,index) in vendor" :key="index">
          <td>{{ v.nama }}</td>
          <td>{{ v.alamat }}</td>
          <td>{{ v.email }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
export default {
  name: 'table',
  data () {
    return {
      alamat: '',
      nama: 'Adinda Yahya Hexatama',
      email: '',
      vendor: []
    }
  },
  beforeCreate () { // 1
    console.log('before-created', this.nama)
  },
  created () { // 2
    this.submitVendor('lalala')
    console.log('created', this.nama)
    this.vendor.push({ 'nama': 'nama-created', 'alamat': 'alamat-created', 'email': 'email-created' })
  },
  beforeMount () { // 3
    console.log('before-mount', this.nama)
  },
  mounted () { // 4
    console.log('mounted', this.nama)
    this.vendor.push({ 'nama': 'nama-mounted', 'alamat': 'alamat-mounted', 'email': 'email-mounted' })
  },
  beforeDestroy () { // 5
    alert('Before-Destroyed')
  },
  destroyed () { // 6
    alert('Destroyed')
  },
  methods: {
    submitVendor (nama) {
      this.vendor.push({ 'nama': nama, 'alamat': this.alamat, 'email': this.email })
      this.nama = ''
      this.alamat = ''
      this.email = ''
    }
  }
}
</script>
