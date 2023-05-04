<template>
  <navbar btn-background="bg-gradient-primary" />
  <div
    class="pt-5 m-3 page-header align-items-start min-vh-50 pb-11 border-radius-lg"  
  >
    <span class="mask bg-gradient-dark opacity-6"></span>
    <div class="container">
      <div class="row justify-content-center">
        <div class="mx-auto text-center col-lg-5">
          <h1 class="mt-5 mb-2 text-white">Đăng ký</h1>
          <p class="text-white text-lead">
            Nhập tên, email và password để đăng ký.
          </p>
        </div>
      </div>
    </div>
  </div>
  <div class="container">
    <div class="row mt-lg-n10 mt-md-n11 mt-n10 justify-content-center">
      <div class="mx-auto col-xl-4 col-lg-5 col-md-7">
        <div class="card z-index-0">
          
          <div class="card-body">
              <SignUpForm :user="user" @submit:user="addUser" />
              <p>{{ message }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
  <app-footer />
</template>

<script>
import Navbar from "@/examples/PageLayout/Navbar.vue";
import AppFooter from "@/examples/PageLayout/Footer.vue";

import UserService from "@/services/user.service";
import SignUpForm from "@/components/SignUpForm.vue";
import * as CryptoJS from 'crypto-js';

export default {
  name: "SignUp",
  components: {
    Navbar,
    AppFooter,
    SignUpForm,
  },
  data() {
      return {
          user: {
              name: null,
              email: null,
              password: null,
              role: 'user'
          },
          message: "",
      };
  },
  methods: {
    async addUser(data) {
            try {
                const passphrase = '123456'
                data.password = CryptoJS.AES.encrypt(data.password, passphrase).toString()
                await UserService.create(data);
                this.message = alert("Đăng ký thành công.");
                this.$router.push({ name: "user" });
            } catch (error) {
                console.log(error);
            }
    },
  },
  created() {
    this.$store.state.hideConfigButton = true;
    this.$store.state.showNavbar = false;
    this.$store.state.showSidenav = false;
    this.$store.state.showFooter = false;
  },
  beforeUnmount() {
    this.$store.state.hideConfigButton = false;
    this.$store.state.showNavbar = true;
    this.$store.state.showSidenav = true;
    this.$store.state.showFooter = true;
  },
};
</script>
