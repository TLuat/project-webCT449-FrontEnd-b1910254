
<template>
  <tr class="cursor-pointer" v-for="(user, index) in users" :key="user._id" @click="updateActiveIndex(index)">
        <td :class="{'bg-primary text-white': user.isActive}"><i class="ni ni-single-02 text-success text-gradient"></i></td>
        <td :class="{'bg-primary text-white': user.isActive}">
          {{user.name }}
        </td>
        <td class="" :class="{'bg-primary text-white': user.isActive}">
          {{ user.email }}
        </td>
  </tr>
</template>

<script>
export default {
  props: {
    users: { type: Array, default: [] },
    activeIndex: { type: Number, default: -1 },
  },
  emits: ["update:activeIndex"],
  methods: {
    updateActiveIndex(index) {
      this.users.forEach((user) => {
        user.isActive = false;
      });
      this.users[index].isActive = true;
      this.$emit("update:activeIndex", index);
    },
  },
  computed: {
    activeUser() {
      if (this.activeIndex < 0) return null;
      return this.filteredUsers[this.activeIndex];
    },
  },
};
</script>