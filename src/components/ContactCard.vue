<template>
  <div>
    <div class="card-body p-3">
      <div class="timeline timeline-one-side">
        <div class="timeline-block mb-3">
          <span class="timeline-step">
            <i class="ni ni-single-02 text-success text-gradient"></i>
          </span>
          <div class="timeline-content">
            <p class="text-secondary font-weight-bold text-xs mt-1 mb-0">Tên</p>
            <h6 class="text-dark text-sm font-weight-bold mb-0">{{ contact.name }}</h6>
          </div>
        </div>
        <div class="timeline-block mb-3">
          <span class="timeline-step">
            <i class="ni ni-email-83 text-danger text-gradient"></i>
          </span>
          <div class="timeline-content">
            <p class="text-secondary font-weight-bold text-xs mt-1 mb-0">Email</p>
            <h6 class="text-dark text-sm font-weight-bold mb-0">{{ contact.email }}</h6>
          </div>
        </div>
        <div class="timeline-block mb-3">
          <span class="timeline-step">
            <i class="ni ni-square-pin text-info text-gradient"></i>
          </span>
          <div class="timeline-content">
            <p class="text-secondary font-weight-bold text-xs mt-1 mb-0">Địa chỉ</p>
            <h6 class="text-dark text-sm font-weight-bold mb-0">{{ contact.address }}</h6>
          </div>
        </div>
        <div class="timeline-block mb-3">
          <span class="timeline-step">
            <i class="ni ni-mobile-button text-warning text-gradient"></i>
          </span>
          <div class="timeline-content">
            <p class="text-secondary font-weight-bold text-xs mt-1 mb-0">Số điện thoại</p>
            <h6 class="text-dark text-sm font-weight-bold mb-0">{{ contact.phone }}</h6>
          </div>
        </div>
        <div class="timeline-block mb-3">
          <span class="timeline-step">
            <i class="ni ni-tag text-primary text-gradient"></i>
          </span>
          <div class="timeline-content">
            <p class="text-secondary font-weight-bold text-xs mt-1 mb-0">Khách hàng quan trọng</p>
            <h6 class="text-dark text-sm font-weight-bold mb-0 ">
              <i v-if="contact.favorite" class="ni ni-check-bold text-primary text-gradient fs-3"></i>
              <i v-else class="ni ni-fat-remove text-primary text-gradient fs-3"></i>
            </h6>
          </div>
          
        </div>
      </div>
    </div>
    
  </div>
</template>

<script>
export default {
  props: {
    contact: { type: Object, required: true },
  },
};
</script>