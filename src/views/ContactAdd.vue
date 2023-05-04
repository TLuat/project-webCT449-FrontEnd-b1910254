<template>
    <div class="page">
        <div>
            <router-link
              class="nav-link d-flex align-items-center me-2 active"
              aria-current="page"
              to="/dashboard"
            >
              <i
                class="ni ni-bold-left"
              ></i>
              Quay lại
            </router-link>
        </div>
        <div class="py-4 container-fluid">
            <h5><i class="ni ni-fat-add text-success fs-2"></i> Thêm Thông tin khách hàng</h5>
            <ContactForm :contact="{}" @submit:contact="addContact"/>
            <p class="text-success">{{ message }}</p>
        </div>
    </div>
</template>

<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";
export default {
    components: {
        ContactForm,
    },
    data() {
        return {
            message: "",
        };
    },
    methods: {
        async addContact(data) {
            try {
                await ContactService.create(data);
                this.message = "Thêm liên hệ thành công.";
            } catch (error) {
                console.log(error);
            }
        }
    },
};
</script>
