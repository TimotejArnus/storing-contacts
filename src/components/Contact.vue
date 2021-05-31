<template>
  <div @dblclick="showEdit()" class="contact">    
    <div class="user">
      <h3>
        {{ contact.name }}
      </h3>
      <i @click="$emit('delete-contact', contact._id)" class="fas fa-times">
      </i>
    </div>
    <div v-if="showEditContact">
      <EditContact :contact="contact"  class="edit" @edit-contact="Edit" />
    </div>
  </div>
</template>

<script>
import EditContact from "./EditContact";

export default {
  name: "Contact",  
  data() {
    return {
      newcontact: EditContact.data.newcontact
    };
  }, 
  props: {
    contact: Object,   
    showEditContact: Boolean,       
  },
  components: {
    EditContact,
  },
  methods:{
    showEdit(){
      this.showEditContact = !this.showEditContact;
    },     
    Edit(newcontact){      
      this.$emit('edit-contact', newcontact)    
    }
  },
    
};
</script>

<style scope>
.fas {
  color: red;
  display: flex;
  text-align: right;
  vertical-align: 30px;
  align-items: center;
  justify-content: space-between;
  cursor: pointer;
}
.contact {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  align-items: center;
  justify-content: space-between;
}
.user {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.edit {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
