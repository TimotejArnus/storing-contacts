<template>
  <header>
    <h1>{{ title }}</h1>
    <Button @btn-click = "$emit('show-add')" :text="showAddContact ? 'Close' : 'Add Contact' " :color="showAddContact ? 'danger' : 'success' "/>
  </header>
</template>

<script>
import Button from "./Button";

export default {
  name: "Header",
  props: {
    title: String,
    showAddContact: Boolean,
  },
  components: {
    Button,
  },
};
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 16px;
}
</style>