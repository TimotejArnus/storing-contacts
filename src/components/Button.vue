<template>
  <b-button class="btn-space" @click="onClick()" :variant="color">{{ text }}</b-button>
</template>

<script>
export default {
  name: "Button",
  props: {
    text: String,
    color: String,
  },
  methods: {
    onClick() {
      this.$emit('btn-click');
    },
  },
};
</script>
