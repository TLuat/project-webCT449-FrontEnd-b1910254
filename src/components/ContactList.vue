<template>
  <tr class="cursor-pointer" v-for="(contact, index) in contacts" :key="contact._id" @click="updateActiveIndex(index)">
    <td :class="{'bg-primary text-white': contact.isActive}">
      {{contact.name }}
    </td>
    <td :class="{'bg-primary text-white': contact.isActive}">
      {{ contact.address }}
    </td>
    <td class="text-center fs-5" :class="{'bg-primary text-white': contact.isActive}">
      <i v-if="contact.favorite" class="ni ni-check-bold text-success text-gradient"></i>
      <i v-else class="ni ni-fat-remove text-success text-gradient"></i>
    </td>
    <td class="text-center" :class="{'bg-primary text-white': contact.isActive}">
      <i class="ni ni-active-40 text-success text-gradient"></i>
    </td>
  </tr>
</template>

<script>
export default {
  props: {
    contacts: { type: Array, default: [] },
    activeIndex: { type: Number, default: -1 },
  },
  emits: ["update:activeIndex"],
  methods: {
    updateActiveIndex(index) {
      // Set isActive property for each contact object
      this.contacts.forEach((contact) => {
        contact.isActive = false;
      });
      this.contacts[index].isActive = true;
      this.$emit("update:activeIndex", index);
    },
  },
  computed: {
    activeContact() {
      if (this.activeIndex < 0) return null;
      return this.filteredContacts[this.activeIndex];
    },
  },
};
</script>
