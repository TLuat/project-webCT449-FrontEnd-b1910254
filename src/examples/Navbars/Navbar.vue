<template>
  <nav
    v-bind="$attrs"
    id="navbarBlur"
    class="shadow-none navbar navbar-main navbar-expand-lg border-radius-xl"
    data-scroll="true"
  >
    <div class="px-3 py-1 container-fluid">
      <ol class="breadcrumb bg-transparent mb-0 pb-0 pt-1 px-0 me-sm-6 me-5">
          <li class="breadcrumb-item text-sm"><a class="opacity-5 text-black" href="javascript:;">Pages</a></li>
          <li class="breadcrumb-item text-sm text-black active" aria-current="page">{{ pagename }}</li>
      </ol>
      <h6 class="mb-0 font-weight-bolder">{{ pagename }}</h6>
      <div
        id="navbar"
        class="mt-2 collapse navbar-collapse mt-sm-0 me-md-0 me-sm-4"
        :class="$store.state.isRTL ? 'px-0' : 'me-sm-4'"
      >
        <div
          class="pe-md-3 d-flex align-items-center"
          :class="$store.state.isRTL ? 'me-md-auto' : 'ms-md-auto'"
        >
        </div>
        <ul class="navbar-nav justify-content-end">
          <li class="nav-item d-flex align-items-center">
            <!-- da dang nhap -->
            <span v-if="isLogin == 'true'" class="">
                <router-link
                :to="{ name: 'Profile' }"
                class="px-0 nav-link font-weight-bold"
                :class="textWhite ? textWhite : 'text-body'"
              >
                <i class="fa fa-user" :class="$store.state.isRTL ? 'ms-sm-2' : 'me-sm-1'"></i>
                <span  class="d-sm-inline d-none">{{ username }}</span>
              </router-link>
            </span>
            <!-- chua dang nhap -->
            <span v-if="isLogin != 'true'">
                <router-link
                :to="{ name: 'Sign In' }"
                class="px-0 nav-link font-weight-bold"
                :class="textWhite ? textWhite : 'text-body'"
              >
                <i class="fa fa-user" :class="$store.state.isRTL ? 'ms-sm-2' : 'me-sm-1'"></i>
                <!-- <span v-if="$store.state.isRTL" class="d-sm-inline d-none">xu ly login</span> -->
                <span  class="d-sm-inline d-none">Đăng nhập</span>
              </router-link>
            </span>
          </li>
          <li class="nav-item d-xl-none ps-3 d-flex align-items-center">
            <a
              id="iconNavbarSidenav"
              href="#"
              class="p-0 nav-link text-body"
              @click="toggleSidebar"
            >
              <div class="sidenav-toggler-inner">
                <i class="sidenav-toggler-line"></i>
                <i class="sidenav-toggler-line"></i>
                <i class="sidenav-toggler-line"></i>
              </div>
            </a>
          </li>
          <li class="px-3 nav-item d-flex align-items-center">
            <a
              class="p-0 nav-link"
              :class="textWhite ? textWhite : 'text-body'"
              @click="toggleConfigurator"
            >
              <i class="cursor-pointer fa fa-cog fixed-plugin-button-nav"></i>
            </a>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>
<script>
import { mapMutations, mapActions } from "vuex";

export default {
  name: "NavbarComponent",
  data() {
    return {
      showMenu: false,
      title: "Vite Soft UI Dashboard",
      controls: "dashboardsExamples",
      isActive: "active",
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
      routename: this.$route.name,
      isLogin: localStorage.getItem('isLogin'),
      username: localStorage.getItem('username'),
      userid: localStorage.getItem('userid'),
      role: localStorage.getItem('role')
    };
  },
  props: {
      modelValue: { type: String, default: "" },
      required: true,
      type: String,
      default: ""
  },
  computed: {
    currentRouteName() {
      return this.$route.name;
    },
  },
  created() {
    this.minNav;
  },
  updated() {
    const navbar = document.getElementById("navbarBlur");
    window.addEventListener("scroll", () => {
      if (window.scrollY > 10 && this.$store.state.isNavFixed) {
        navbar.classList.add("blur");
        navbar.classList.add("position-sticky");
        navbar.classList.add("shadow-blur");
      } else {
        navbar.classList.remove("blur");
        navbar.classList.remove("position-sticky");
        navbar.classList.remove("shadow-blur");
      }
    });
  }, methods: {
    ...mapMutations(["navbarMinimize", "toggleConfigurator"]),
    ...mapActions(["toggleSidebarColor"]),

    toggleSidebar() {
      this.toggleSidebarColor("bg-white");
      this.navbarMinimize();
    },
  },
};
</script>
