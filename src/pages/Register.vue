<template>
  <q-page class="bg-grey-3">
    <div class="row">
      <q-card class="fixed-center col-md-4 col-xs-12 bg-white" flat>
        <q-card-section>
          <div class="text-h6 q-pb-md">
            Halaman Register Pasien App
          </div>
          <q-form
            @submit="onSubmit"
            @reset="onReset"
            class="q-gutter-md"
          >
            <q-input
              filled
              v-model="username"
              label="Username Anda"
              lazy-rules
              :rules="[ val => val && val.length > 0 || 'Tolong Ketik Username']"
            />

            <q-input
              filled
              v-model="namaLengkap"
              label="Nama Lengkap Anda"
              lazy-rules
              :rules="[ val => val && val.length > 0 || 'Tolong Ketik Nama Lengkap']"
            />

             <q-input
              filled
              v-model="email"
              label="E-Mail Anda"
              lazy-rules
              :rules="[ val => val && val.length > 0 || 'Tolong Ketik E-Mail']"
            />

            <q-input
              filled
              type="password"
              v-model="password"
              label="Password Anda"
              lazy-rules
              :rules="[
                val => val !== null && val.length > 0 || 'Password Tidak Boleh Kosong'
              ]"
            />
            <div class="q-gutter-md">
              <q-btn label="Register" type="submit" color="primary"/>
              <q-btn label="Login" to="/" flat color="primary"/>
            </div>
        </q-form>
        </q-card-section>
    </q-card>
    </div>
  </q-page>
</template>
<script>
export default {
  data () {
    return {
      username: null,
      password: null,
      namaLengkap: null,
      email: null
    }
  },
  methods: {
    onSubmit () {
      this.$axios.post('user/register', {
        username: this.username,
        password: this.password,
        namaLengkap: this.namaLengkap,
        email: this.email
      }).then((res) => {
        if (res.data.sukses) {
          this.$showNotif(res.data.pesan, 'positive')
          this.$router.push({ name: 'loginPage' })
        } else {
          this.$showNotif(res.data.pesan, 'negative')
        }
      })
    },
    onReset () {
      this.username = null
      this.password = null
    }
  }
}
</script>
