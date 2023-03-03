<template>
  <q-layout view="hHh lpR fF2">
    <q-page class="main-page column items-center">
      <div
        class="logo q-mt-lg"
        style="
          width: 312px;
          height: 70px;
          background-color: #d9d9d9;
          border-radius: 15px;
        "
      ></div>
      <div
        class="q-mt-xl"
        style="
          width: 965px;
          height: 791px;
          background-color: #d9d9d9;
          border-radius: 15px;
          position: relative;
        "
      ></div>
      <div class="login-form">
        <div
          class="row justify-between items-end q-px-sm"
          style="margin-top: 176px"
        >
          <p class="jakarta-sb q-mb-none" style="font-size: 36px">Masuk</p>
          <p
            class="jakarta-sb q-mb-none"
            style="font-size: 24px; color: #58936e"
          >
            Daftar
          </p>
        </div>
        <q-form @submit="submit">
          <p
            class="jakarta-sb q-mb-none q-px-sm q-mt-xl"
            style="font-size: 16px; color: #116530"
          >
            Username
          </p>
          <q-input
            outlined
            round
            v-model="username"
            class="q-mt-sm"
          />
          <p
            class="jakarta-sb q-mb-none q-px-sm q-mt-md"
            style="font-size: 16px; color: #116530"
          >
            Password
          </p>
          <q-input
            class="q-mt-sm"
            outlined
            v-model="password"
            :type="isPwd ? 'password' : 'text'"
          >
            <template v-slot:append>
              <q-icon
                :name="isPwd ? 'visibility_off' : 'visibility'"
                class="cursor-pointer"
                @click="isPwd = !isPwd"
              />
            </template>
          </q-input>
          <div class="row justify-between items-end q-mt-lg">
            <q-checkbox size="55px" v-model="orange" label="Ingat Saya" />
            <q-btn
              flat
              label="Lupa Kata Sandi?"
              no-caps
              style="color: #58936e"
              size="16px"
            />
          </div>
          <q-btn
            class="jakarta-b q-mt-xl q-mb-md"
            type="submit"
            unelevated
            style="
              background: #116530;
              width: 100%;
              height: 56px;
              border-radius: 15px;
              font-size: 24px;
            "
            label="Masuk"
            text-color="white"
            no-caps
          />
        </q-form>
        <div class="row items-center justify-center">
          <p class="jakarta-sb q-mb-none q-pa-none">Butuh Bantuan?</p>
          <q-btn
            flat
            label="Hubungi Buah.in Care"
            no-caps
            style="color: #58936e"
            class="q-pa-none"
          />
        </div>
      </div>
    </q-page>
  </q-layout>
</template>

<script>
import { ref } from "vue";

export default {
  name: "Login",

  data() {
    return {
      username: ref(null),
      password: ref(null),
      isPwd: ref(true),
      orange: ref(false),
    };
  },

  methods: {
    submit() {
      const userData = {
        username: this.username,
        password: this.password,
      };
      console.log(userData);
    }
  }
};
</script>

<style>
.main-page {
  background-color: #f5f5f5;
  height: min-content;
}

.login-form {
  width: 584px;
  height: 848px;
  background-color: white;
  position: relative;
  bottom: 815px;
  padding: 0 44px;
  border-radius: 25px;
}
</style>
