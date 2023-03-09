<template>
  <q-layout view="hHh lpR fF2">
    <q-page class="main-page column items-center">
      <q-img class="q-mt-lg" src="icons/logo.png" style="width: 322px; height: 72px;" />
      <div class="row justify-evenly q-mt-xl" style="width: 100%">
        <q-img src="icons\resgistration.png" style="width: 581px; height: 624px;" />
        <div class="register-form">
          <P class="jakarta-sb q-mb-none q-mt-xl" style="font-size: 36px; text-align: center">Daftar Sekarang</P>
          <div class="row items-center justify-center">
            <P class="jakarta-r q-mb-none" style="font-size: 24px; text-align: center">Sudah punya akun Buah.in?</P>
            <q-btn flat label="Masuk" no-caps style="color: #58936e" class="q-pa-none" size="28px" />
          </div>
          <q-form @submit.prevent="submit">
            <p class="jakarta-sb q-mb-none q-px-sm q-mt-xl" style="font-size: 16px; color: #116530">
              Username
            </p>
            <q-input outlined round v-model="Username" class="q-mt-sm" :rules="[(val) => !!val]" />
            <p class="jakarta-sb q-mb-none q-px-sm q-mt-md" style="font-size: 16px; color: #116530">
              Password
            </p>
            <q-input class="q-mt-sm" outlined v-model="Password" :type="isPwd ? 'password' : 'text'" :rules="[
              (val) => !!val,
              (val) =>
                val.length <= 8 ||
                'Password maksimial terdiri dari 8 karakter',
            ]">
              <template v-slot:append>
                <q-icon :name="isPwd ? 'visibility_off' : 'visibility'" class="cursor-pointer" @click="isPwd = !isPwd" />
              </template>
            </q-input>
            <p class="jakarta-sb q-mb-none q-px-sm" style="font-size: 16px; color: #116530">
              Email
            </p>
            <q-input outlined round v-model="Email" class="q-mt-sm" :rules="[(val) => !!val]" />
            <p class="jakarta-sb q-mb-none q-px-sm q-mt-md" style="font-size: 16px; color: #116530">
              Nomor Telepon
            </p>
            <q-input outlined round v-model="noTelp" class="q-mt-sm" :rules="[(val) => !!val]" />
            <q-btn class="jakarta-b q-mt-xl q-mb-md" type="submit" unelevated style="
                  background: #116530;
                  width: 100%;
                  height: 56px;
                  border-radius: 15px;
                  font-size: 24px;
                " label="Daftar" text-color="white" no-caps />
          </q-form>
          <div class="row items-center justify-center">
            <P class="jakarta-sb q-mb-none q-mx-xs">Dengan mendaftar saya menyetujui</P>
            <q-btn flat label="Syarat dan Ketentuan" no-caps style="color: #58936e" class="q-pa-none" />
            <P class="jakarta-sb q-mb-none q-mx-xs">serta</P>
            <q-btn flat label="Kebijakan Privasi" no-caps style="color: #58936e" class="q-pa-none" />
          </div>
        </div>
      </div>
    </q-page>
  </q-layout>
</template>

<script>
// import { Notify } from 'quasar'
import { ref } from "vue";
import { api } from "src/boot/axios";

export default {
  name: "Register",

  data() {
    return {
      Username: ref(null),
      Password: ref(null),
      isPwd: ref(true),
      Email: ref(null),
      noTelp: ref(null),
    };
  },

  methods: {
    async submit() {
      const userData = {
        Username: this.Username,
        Password: this.Password,
        Email: this.Email,
        noTelp: this.noTelp,
      }
      // await api.post('/register', userData).then((response)=>{
      //   console.log(response);
      // })

      // if(res.data.error) {
      //   this.$q.notify({
      //     color: 'negative',
      //     message: res.data.msg,
      //     icon: 'ion-close'
      //   })
      // } else {
      //   this.$q.notify({
      //     color: 'positive',
      //     message: res.data.msg,
      //     icon: 'ion-close'
      //   })
      //   this.$router.push('/')
      // }

    },
  },
};
</script>

<style>
.main-page {
  padding: 0 160px;
  background-color: #f5f5f5;
  height: min-content;
}

.register-form {
  width: 546px;
  height: 795px;
  background-color: white;
  padding: 0 24px;
  border-radius: 25px;
}
</style>
