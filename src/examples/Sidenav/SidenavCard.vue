<template>
  <div id="sidenavCard" class="shadow-none card card-background card-background-mask-secondary">
    
  </div>
</template>
<script>
import imgWhiteCurved from "../../assets/img/curved-images/white-curved.jpeg";
export default {
  name: "SidenavCard",
  props: {
    textPrimary: {
      type: String,
      default: ""
    },
    textSecondary: {
      type: String,
      default: ""
    },
    href: {
      type: String,
      default: ""
    },
    linkText: {
      type: String,
      default: ""
    },
    iconClass: {
      type: String,
      default: ""
    },
  },
  data() {
    return {
      imgWhiteCurved,
    };
  },
};
</script>
