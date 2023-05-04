<template>
  <div class="py-4 container-fluid">
    <div class="row page">
      <!-- abc -->
      <button class="btn btn-primary px-3 mx-2 rounded-5" style="width: 20%;" @click="refreshList()">
        <i class="fas fa-redo"> Làm mới</i>
      </button>
      <button class="btn btn-success px-3 mx-2 rounded-5" style="width: 20%;" @click="goToAddContact">
        <i class="fas fa-plus"> Thêm mới</i>
      </button>
      <button class="btn btn-danger px-3 mx-2 rounded-5" style="width: 20%;" @click="removeAllContacts">
        <i class="fas fa-trash"> Xóa tất cả</i>
      </button>
    </div>
    <!-- tìm kiếm -->
    <div class="row my-4">
      <div class="col-lg-8 col-md-6 mb-md-0 mb-4">
        <InputSearch v-model="searchText" />
      </div>
      <div class="col-lg-4 col-md-6">
        <div class="card h-100 p-2">
          <h4 class="text-center">
              <i class="ni ni-badge text-success text-gradient"></i>
              <h6 class="d-inline-block text-center"> Chi tiết khách hàng</h6>
          </h4>
        </div>
      </div>
    </div>
    <!-- Cart 1 -->
    <div class="row my-4">
      <div class="col-lg-8 col-md-6 mb-md-0 mb-4">

        <div class="card">
          <div class="card-header pb-0">

            <div class="row">
              <div class="col-lg-6 col-7 fs-4">
                <i class="ni ni-briefcase-24 text-success text-gradient"></i> Danh sách khách hàng
              </div>
              
              <!-- Dropdown -->
                <div class="col-lg-6 col-5 my-auto text-end">
                  <DropDownSearch v-model="searchText" />
                </div>

            </div>
          </div>
          <div class="card-body px-0 pb-2">
            <div class="table-responsive">
              <table class="table align-items-center mb-0">
                <thead>
                  <tr>
                    <th class="text-uppercase text-secondary text-xxs font-weight-bolder opacity-7">
                      Tên
                    </th>
                    <th class="text-uppercase text-secondary text-xxs font-weight-bolder opacity-7 ps-2">
                      Địa chỉ
                    </th>
                    <th class="text-center text-uppercase text-secondary text-xxs font-weight-bolder opacity-7">
                      Quan trọng
                    </th>
                    <th class="text-center text-uppercase text-secondary text-xxs font-weight-bolder opacity-7">
                      Chọn
                    </th>
                  </tr>
                </thead>
                <!-- <tbody> -->
                <tbody class="text-sm mb-0">
                  <ContactList v-if="filteredContactsCount > 0" :contacts="filteredContacts"
                    v-model:activeIndex="activeIndex" />
                  <p v-else>Không có khách hàng nào.</p>   
                </tbody>
              </table>
            </div>
          </div>
        </div>
      </div>
      <div class="col-lg-4 col-md-6">
        <div class="card h-100 p-2">
          <div class="card-header pb-0" v-if="activeContact">
            
            <ContactCard :contact="activeContact" />

            <router-link :to="{
                name: 'contact.edit',
                params: { id: activeContact._id },
              }">
            <i class="ni ni-settings text-warning text-gradient"></i>
              Chỉnh sửa
            </router-link>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import setTooltip from "@/assets/js/tooltip.js";

import ContactCard from "@/components/ContactCard.vue";
import InputSearch from "@/components/InputSearch.vue";
import DropDownSearch from "@/components/DropDownSearch.vue";
import ContactList from "@/components/ContactList.vue";
import ContactService from "@/services/contact.service";

export default {
  name: "DashboardDefault",
  components: {
    ContactCard,
    InputSearch,
    DropDownSearch,
    ContactList,

  },
  data() {
    return {
      contacts: [],
      activeIndex: -1,
      searchText: "",
    };
  },
  watch: {
    // Giám sát các thay đổi của biến searchText.
    // Bỏ chọn phần tử đang được chọn trong danh sách.
    searchText() {
      this.activeIndex = -1;
    },
  },
  computed: {
    // Chuyển các đối tượng contact thành chuỗi để tiện cho tìm kiếm.
    contactStrings() {
      return this.contacts.map((contact) => {
        const { name, email, address, phone, favorite } = contact;
        return [name, email, address, phone, favorite].join("");  
      });
    },
    // Trả về các contact có chứa thông tin cần tìm kiếm.
    filteredContacts() {
      if (!this.searchText) return this.contacts;
      return this.contacts.filter((_contact, index) =>
        this.contactStrings[index].includes(this.searchText)
      );
    },
    activeContact() {
      if (this.activeIndex < 0) return null;
      return this.filteredContacts[this.activeIndex];
    },
    filteredContactsCount() {
      return this.filteredContacts.length;
    },
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
      if (confirm("Bạn muốn xóa tất cả Khách hàng?")) {
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
    setTooltip();
    this.refreshList();
  },  
};
</script>
