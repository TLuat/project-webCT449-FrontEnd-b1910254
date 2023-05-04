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
  <div class="">
    <div class="float-lg-end pe-4">
      <div class=" px-2 py-3 ms-sm-n4 ms-n5" aria-labelledby="dropdownTable">
        <select class="form-select" aria-label="Default select example"
        :value="modelValue" 
        @input="updateModelValue"
        @keyup.enter="submit"
        >
          <option value="">Tất cả</option>
          <option value="true">Quan trọng</option>
          <option value="false">Bình thường</option>
        </select>
      </div>
    </div>
  </div>
</template>
