<template>
  <div class="forum">
    <b-form @submit="onSubmit">
      <b-form-group id="input-group-1" label="Name:" label-for="input-1">
        <b-form-input
          id="input-1"
          v-model="newcontact.name"        
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group
        id="input-group-2"
        label="Email address:"
        label-for="input-2"
      >
        <b-form-input
          id="input-2"
          v-model="newcontact.email"
          type="email"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group
        id="input-group-3"
        label="Phone number:"
        label-for="input-3"
      >
        <b-form-input
          id="input-3"
          v-model="newcontact.phone"          
          required
        ></b-form-input>
      </b-form-group>     

      <b-button type="submit" variant="info" style="margil-right: 5px"
        >Change</b-button
      >
    </b-form>
  </div>
</template>


<script>
export default {
  name: "AddContact",
  props: {
    contact: Object,    
  },
  data() {
    return {
      newcontact: {
        id: this.contact._id,
        name: this.contact.name,
        email: this.contact.email,        
        phone: this.contact.phone,
      },    
    };
  },
  methods: {
    onSubmit(event) {
      event.preventDefault(); 
      this.$emit('edit-contact', this.newcontact);
    },
  },
};
</script>

<style>
.forum{
  user-select: none;
}
</style>
