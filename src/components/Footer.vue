<template>
  <footer>
    <p>Copyright &copy; 2021</p>
    <div class="link" @click="redirectUser()">Sign out</div>
  </footer>
</template>

<script>
export default {
  name: "Login",
  methods: {
    redirectUser() {
      localStorage.removeItem("jwt");
      this.$router.push("/login");
    },
  },
};
</script>

<style scoped>
.link {
  cursor: pointer;
}

.link:hover {
  text-decoration: underline;
}
a {
  color: #333;
}

footer {
  margin-top: 24px;
  text-align: center;
}
</style>