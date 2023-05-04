<template>
  <div class="container top-0 position-sticky z-index-sticky">
    <div class="row">
      <div class="col-12">
        <navbar
          is-blur="blur blur-rounded my-3 py-2 start-0 end-0 mx-4 shadow"
          btn-background="bg-gradient-success"
          :dark-mode="true"
        />
      </div>
    </div>
  </div>
  <main class="mt-0 main-content main-content-bg">
    <section>
      <div class="page-header min-vh-75">
        <div class="container">
          <div class="row">
            <div class="mx-auto col-xl-4 col-lg-5 col-md-6 d-flex flex-column">
              <div class="mt-8 card card-plain">
                <div class="pb-0 card-header text-start">
                  <h3 class="font-weight-bolder text-info text-gradient">Đăng nhập </h3>
                  <p class="mb-0">Nhập email và mật khẩu để đăng nhập</p>
                </div>
                <div class="card-body">
                  <SignInForm :user="user" @submit:user="checkUser" />
                  <p>{{ message }}</p>
                </div>
                <div class="px-1 pt-0 text-center card-footer px-lg-2">
                  <p class="mx-auto mb-4 text-sm">
                    Chưa có tài khoản?
                    <a
                      href="javascript:;"
                      class="text-info text-gradient font-weight-bold"
                    >Đăng ký</a>
                  </p>
                </div>
              </div>
            </div>
            
          </div>
        </div>
      </div>
    </section>
  </main>
  <app-footer />
</template>

<script>
import Navbar from "@/examples/PageLayout/Navbar.vue";
import AppFooter from "@/examples/PageLayout/Footer.vue";
import bgImg from "@/assets/img/curved-images/curved9.jpg"
import SignInForm from "@/components/SignInForm.vue";

import UserService from "@/services/user.service";
import * as CryptoJS from 'crypto-js';

import { Form, Field, ErrorMessage } from "vee-validate";

const body = document.getElementsByTagName("body")[0];

export default {
  name: "SigninPage",
  components: {
    Navbar,
    AppFooter,
    SignInForm,
    Form,
    Field,
    ErrorMessage,
  },
  emits: ["submit:user", "delete:user"],
  data() {
      return {
        bgImg,
        users: {
            name: null,
            email: null,
            password: null,
        },
        user: {
            name: null,
            email: null,
            password: null,
        },
        message: "",
      };
  },
  methods: {
    async checkUser(data) {
            try {
                const passphrase = '123456'

                this.users = await UserService.getAll();

                for (var i = 0; i < this.users.length; i++) {

                        if (this.users[i].email != data.email) {
                            this.message = "Email không tồn tại .";
                        }
                        else {
                            const bytes = CryptoJS.AES.decrypt(this.users[i].password, passphrase)
                            this.users[i].password = bytes.toString(CryptoJS.enc.Utf8)
                            if (this.users[i].password != data.password) {
                                this.message = "Mật khẩu sai .";
                            }
                            else {
                                this.message = "Đăng nhập thành công .";
                                localStorage.setItem('username', this.users[i].name);
                                localStorage.setItem('email', this.users[i].email);
                                localStorage.setItem('userid', this.users[i]._id);
                                localStorage.setItem('isLogin', true);
                                
                                this.$router.push({ name: "Dashboard" });
                                break;
                            }
                        }
                    
                }
            } catch (error) {
                console.log(error);
            }
        },
  },
  beforeMount() {
    this.$store.state.hideConfigButton = true;
    this.$store.state.showNavbar = false;
    this.$store.state.showSidenav = false;
    this.$store.state.showFooter = false;
    body.classList.remove("bg-gray-100");
  },
  beforeUnmount() {
    this.$store.state.hideConfigButton = false;
    this.$store.state.showNavbar = true;
    this.$store.state.showSidenav = true;
    this.$store.state.showFooter = true;
    body.classList.add("bg-gray-100");
  },
};
</script>
