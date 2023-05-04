<template>
  <div class="py-4 container-fluid">

    <!-- Cart 1 -->
    <div class="row my-4">
      <div class="col-lg-8 col-md-6 mb-md-0 mb-4">

        <div class="card">
          <div class="card-header pb-0">

            <div class="row">
              <div class="col-lg-6 col-7">
                <h6>Thông tin tài khoản cá nhân</h6>
              </div>
              <p class="card-text"> <i class="ni ni-single-02 text-success text-gradient"></i> Tên: {{ username }}</p>
              <p class="card-text"><i class="ni ni-email-83 text-danger text-gradient"></i> Email: {{ email }}</p>
            </div>
          </div>
          <div class="card-body px-0 pb-2">
            <div class="table-responsive">
              
            </div>
          </div>
        </div>
      </div>
      <div class="col-lg-4 col-md-6">
        
      </div>
    </div>
  </div>
</template>
<script>

import ContactCard from "@/components/ContactCard.vue";
import InputSearch from "@/components/InputSearch.vue";
import ContactList from "@/components/ContactList.vue";
import ContactService from "@/services/contact.service";

export default {
  name: "DashboardDefault",
  components: {
    ContactCard,
    InputSearch,
    ContactList,
  },
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
      email: localStorage.getItem('email'),
      userid: localStorage.getItem('userid'),
      role: localStorage.getItem('role')
    };
  },
  methods: {
    async retrieveContacts() {
      try {
        this.contacts = await ContactService.getAll();
      } catch (error) {
        console.log(error);
      }
    },
    refreshList() {
      this.retrieveContacts();
      this.activeIndex = -1;
    },
    async removeAllContacts() {
      if (confirm("Bạn muốn xóa tất cả Liên hệ?")) {
        try {
          await ContactService.deleteAll();
          this.refreshList();
        } catch (error) {
          console.log(error);
        }
      }
    },
    goToAddContact() {
      this.$router.push({ name: "contact.add" });
    },
  },
  mounted() {
    this.refreshList();
  },  
};
</script>
