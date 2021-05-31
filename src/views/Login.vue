<template>
  <div class="container">
    <h1>Login</h1>

    <b-form class="space" @submit="onSubmit" @reset="onReset">
      <b-form-group id="input-group-1" label="Your Email:" label-for="input-1">
        <b-form-input
          id="input-1"
          v-model="user.email"
          placeholder="Enter Email"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group
        id="input-group-2"
        label="Your Password:"
        label-for="input-2"
      >
        <b-form-input
          id="input-2"
          v-model="user.password"
          placeholder="Enter Password"
          required
        ></b-form-input>
      </b-form-group>
      <b-button type="submit" variant="primary">Submit</b-button>
    </b-form>
    <router-link class="link" to="/Registration">Register</router-link>
  </div>
</template>

<script>
export default {
  name: "Login",
  data() {
    return {
      user: {
        email: "",
        password: "",
      },
    };
  },
  methods: {
    async onSubmit(event) {
      event.preventDefault();      
      const res = await fetch("http://localhost:5000/login", {
        method: "POST",
        mode: "cors",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify({
          email: this.user.email,
          password: this.user.password,
        }),
      });
      

      if (res.status == 200) {
        const data = await res.json();
        localStorage.setItem("jwt", "Bearer " + data.accessToken);
        this.$router.push("/");
      } else {
        alert("Error");
      }

      // console.log(data.accessToken);

      //   res.status == 200
      //       ? (this.contacts = this.contacts.filter(
      //           (contact) => contact._id !== id
      //         ))
      //       : alert("Error deleting contact");

      // res.status == 200 ? ('jwt', localStorage.setItem('jwt') )

      //   localStorage.setItem( 'token', JSON.stringify(r.token) );

      // TODO ... jwt .. autenticate in router, redirect
      // this.$emit('add-contact', newContact)
      // this.onReset(event)
    },
    onReset(event) {
      event.preventDefault();
      // Reset our form values
      this.user.email = "";
      this.user.name = "";
      // Trick to reset/clear native browser form validation state
    },
  },
};
</script>

<style scoped>
.container {
  text-align: center;
  justify-content: space-around;
}

.space {
  margin: 24px;
}
</style>