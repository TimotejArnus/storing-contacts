<template>
  <div id="app">
    <b-container>
      <Header
        @show-add="showAdd"
        title="Contacts"
        :showAddContact="showAddContact"
      />
      <div v-if="showAddContact">
        <AddContact @add-contact="addContact" />
      </div>
      <hr />
      <Contacts
        @edit-contact="editContact"
        @delete-contact="deleteContact"
        :contacts="contacts"
      />
      <Footer />
    </b-container>
  </div>
</template>

<script>
import Header from "../components/Header";
import Footer from "../components/Footer";
import Contacts from "../components/Contacts";
import AddContact from "../components/AddContact";

export default {
  name: "App",
  components: {
    Header,
    Footer,
    Contacts,
    AddContact,
  },
  foo(){
    console.log("foo")
  },
  
  data() {
    return {
      contacts: [],
      showAddContact: false,
    };
  },
  methods: {
    showAdd() {
      this.showAddContact = !this.showAddContact;
    },
    async addContact(contact) {      
      const res = await fetch("http://localhost:4000/addContact", {
        method: "POST",
        headers: {
          "Content-type": "application/json",
          authorization: localStorage.getItem("jwt"),
        },
        body: JSON.stringify(contact),
      });
      this.showAdd();

       if (this.contacts.length == undefined) {
         this.contacts = []
        
      }

      const data = await res.json();
      this.contacts = [...this.contacts, data];

     
    },
    async deleteContact(id) {
      console.log(id);
      if (confirm("Are you sure you want to delete this contact?")) {
        const res = fetch(`http://localhost:4000/contacts/${id}`, {
          method: "DELETE",
          headers: {
            "Content-type": "application/json",
            authorization: localStorage.getItem("jwt"),
          },
        });

        if ((await res).status) {
          this.contacts = this.contacts.filter((contact) => contact._id !== id);
        } else {
          console.log("err");
        }
      }
    },
    async editContact(newcontact) {
      
      const res = await fetch(
        `http://localhost:4000/contacts/${newcontact.id}`,
        {
          method: "put",
          headers: {
            "Content-type": "application/json",
            authorization: localStorage.getItem("jwt"),
          },
          body: JSON.stringify(newcontact),
        }
      );
      console.log(await res);

      // const data = await res.json();
      // return data;
      // this.contacts = this.contacts.map((
      //   contact // TODO ...
      // ) =>
      //   contact._id == id
      //     ? { ...contact, favorite: !contact.favorite }
      //     : contact
      // ); // change here for edit
    },
    async fetchData() {
      const res = await fetch("http://localhost:4000/contacts", {
        headers: {
          authorization: localStorage.getItem("jwt"),
        },
      });
      const data = await res.json();
      console.log(data.length);
      return data;
    },
  },
  async created() {
    const data = await this.fetchData();
    // if (data.length == undefined)
    //   this.contacts = []
    this.contacts = data
  },
};
</script>

<style>
</style>
