<script>
export default {
  props: {
    modelValue: { type: String, default: "" },
  },
  emits: ["submit", "update:modelValue"],
  methods: {
    updateModelValue(e) {
      this.$emit("update:modelValue", e.target.value);
    },
    submit() {
      this.$emit("submit"); 
    },
  },
};
</script>
<template>
  <div class="input-group">
    <span class="input-group-text text-body">
      <i class="fas fa-search" aria-hidden="true"></i>
    </span>
    <input
      type="text"
      class="form-control"
      placeholder="Nhập thông tin cần tìm"
      :value="modelValue"
      @input="updateModelValue"
      @keyup.enter="submit"
      style="width: 20px; display: inline-block;"
    />
  </div>
</template>
