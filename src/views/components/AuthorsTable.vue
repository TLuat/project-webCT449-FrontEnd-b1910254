<template>
  <div class="card mb-4">
    <div class="card-header pb-0">
      <h4> <i class="ni ni-collection text-success text-gradient"></i> Các thành viên quản lý trên trang web</h4>
      <div class="col-md-10">
        <InputSearch v-model="searchText" />
    </div>
    </div>
    <div class="card-body px-0 pt-0 pb-2">
      <div class="table-responsive p-0">
        <table class="table align-items-center mb-0">
          <thead>
            
            <tr>
              <th class="text-uppercase text-secondary text-xxs font-weight-bolder opacity-7">Logo</th>
              <th
                class="text-uppercase text-secondary text-xxs font-weight-bolder opacity-7 ps-2"
              >Tên</th>
              <th
                class="text-center text-uppercase text-secondary text-xxs font-weight-bolder opacity-7"
              >Email</th>
            </tr>
          </thead>
          <tbody>

            <UserList v-if="filteredUsersCount > 0" :users="filteredUsers"
                    v-model:activeIndex="activeIndex" />
                  <p v-else>Không có liên hệ nào.</p>  

          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>


import InputSearch from "@/components/InputSearch.vue";
import UserService from "@/services/user.service";
import UserList from "@/components/UserList.vue";

export default {
  name: "DashboardDefault",
  components: {
    InputSearch,
    UserList
  },
  data() {
    return {
      users: [],
      activeIndex: -1,
      searchText: "",
    };
  },
  watch: {
    searchText() {
      this.activeIndex = -1;
    },
  },
  computed: {
    contactStrings() {
      return this.users.map((user) => {
        const {name, email } = user;
        return [name, email].join("");
      });
    },
    // Trả về các user có chứa thông tin cần tìm kiếm.
    filteredUsers() {
      if (!this.searchText) return this.users;
      return this.users.filter((_user, index) =>
        this.userStrings[index].includes(this.searchText)
      );
    },
    activeUser() {
      if (this.activeIndex < 0) return null;
      return this.filteredUsers[this.activeIndex];
    },
    filteredUsersCount() {
      return this.filteredUsers.length;
    },
  },
  methods: {
    async retrieveUsers() {
      try {
        this.users = await UserService.getAll();
      } catch (error) {
        console.log(error);
      }
    },
    refreshList() {
      this.retrieveUsers();
      this.activeIndex = -1;
    },
  },
  mounted() {
    this.refreshList();
  },  
};
</script>