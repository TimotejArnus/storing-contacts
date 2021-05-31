<template>
  <div>
    <b-form @submit="onSubmit" @reset="onReset">

        <b-form-group id="input-group-1" label="Your Name:" label-for="input-1">
        <b-form-input
          id="input-1"
          v-model="contact.name"
          placeholder="Enter name"
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
          v-model="contact.email"
          type="email"
          placeholder="Enter email"
          required
        ></b-form-input>
      </b-form-group>      

      <b-form-group id="input-group-3" label="Your Phone number:" label-for="input-3">
        <b-form-input
          id="input-3"
          v-model="contact.phone"
          placeholder="Enter phone"
          required
        ></b-form-input>
      </b-form-group>     

      <b-button type="submit" variant="success" style="margil-right:5px">Add</b-button>
      <!-- <b-button type="reset" variant="danger">Reset</b-button> -->
    </b-form>
    </div>
</template>


<script>
  export default {
    name: 'AddContact',
    data() {
      return {
        contact: {
          email: '',
          name: '',
          phone: '',         
        },  
      }
    },
    methods: {
      onSubmit(event) {
        event.preventDefault()
        const newContact = {
            name: this.contact.name,
            email: this.contact.email,
            phone: this.contact.phone,
        }

        this.$emit('add-contact', newContact)
        this.onReset(event)
        
      },
      onReset(event) {
        event.preventDefault()
        // Reset our form values
        this.contact.email = ''
        this.contact.name = ''
        this.contact.phone = ''
                // Trick to reset/clear native browser form validation state
        
      }
    }
  }
</script>
