<template>
  <div
    id="sidenav-collapse-main"
    class="w-auto h-auto collapse navbar-collapse max-height-vh-100 h-100"
  >
    <ul class="navbar-nav">
      <li class="nav-item">
        <sidenav-collapse nav-text="Giới thiệu" :to="{ name: 'About' }">
          <template #icon>
            <icon name="dashboard" />
          </template>
        </sidenav-collapse>
      </li>

      <li class="nav-item">
        <sidenav-collapse nav-text="Quản lý" :to="{ name: 'Dashboard' }">
          <template #icon>
            <icon name="billing" />
          </template>
        </sidenav-collapse>
      </li>

      <li class="nav-item">
        <sidenav-collapse nav-text="Thành viên" :to="{ name: 'Tables' }">
          <template #icon>
            <icon name="tables" />
          </template>
        </sidenav-collapse>
      </li>

      <li class="mt-3 nav-item">
        <h6
          class="text-xs ps-4 text-uppercase font-weight-bolder opacity-6"
          :class="$store.state.isRTL ? 'me-4' : 'ms-2'"
        >Tài Khoản</h6>
      </li>
      
      <div >

        <!-- chua dn -->
        <span v-if="isLogin != 'true'">
            <li class="nav-item">
              <sidenav-collapse nav-text="Đăng nhập" :to="{ name: 'Sign In' }"
              :class="{ active: this.$route.name == 'Sign In', 'active': this.$route.name == 'Sign In' }">
                <template #icon>
                  <icon name="sign-in" />
                </template>
              </sidenav-collapse>
            </li>
            <li class="nav-item">
              <sidenav-collapse nav-text="Đăng ký" :to="{ name: 'Sign Up' }">
                <template #icon>
                  <icon name="sign-up" />
                </template>
              </sidenav-collapse>
            </li>
        </span>
        <!-- da dang nhap -->
        <span v-if="isLogin == 'true'">
          <li class="nav-item">
            <sidenav-collapse nav-text="Hồ sơ" :to="{ name: 'Profile' }">
              <template #icon>
                <icon name="customer-support" />
              </template>
            </sidenav-collapse>
          </li>
          <li class="nav-item">
            <sidenav-collapse nav-text="Đăng xuất" :to="{ name: 'Sign In' }" @click="logOut">
              <template #icon>
                <icon name="sign-up" />
              </template>
            </sidenav-collapse>
          </li>
        </span>

      </div>
    </ul>
  </div>
</template>
<script>
import Icon from "@/components/Icon.vue";
import SidenavCollapse from "./SidenavCollapse.vue";
import SidenavCard from "./SidenavCard.vue";

export default {
  name: "SidenavList",
  components: {
    Icon,
    SidenavCollapse,
    SidenavCard,
  },
  props: {
    cardBg: {
      type: String,
      default: ""
    },
  },
  data() {
    return {
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
  methods: {
    getRoute() {
      const routeArr = this.$route.path.split("/");
      return routeArr[1];
    },

    logOut() {
            localStorage.removeItem('username');
            localStorage.removeItem('userid');
            localStorage.removeItem('role');
            localStorage.setItem('isLogin', false);

            this.isLogin = 'false'
            this.username = localStorage.getItem('username')

            this.$router.push({ name: "Sign In" });

            this.$forceUpdate();
    },
  },
};
</script>
