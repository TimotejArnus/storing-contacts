<template>
  <div>
    <div v-for="contact in contacts" :key="contact._id">
      <Contact
      :contact="contact"
        @edit-contact="Edit"
        @delete-contact="$emit('delete-contact', contact._id)"
        
      />
    </div>
  </div>
</template>

<script>
import Contact from "./Contact";

export default {
  name: "Contacts",
  data() {
      return {
          newcontact: Contact.EditContact.data.newcontact
      }
    },
  props: {
    contacts: Array,        
  },
  components: {
    Contact,
  },
  // emits: ["delete-contact, edit-contact"],
  methods:{
    Edit(newcontact){      
      this.$emit('edit-contact', newcontact);
    }
  }
};
</script>

<style scoped>
h3 {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 16px;
}
</style>