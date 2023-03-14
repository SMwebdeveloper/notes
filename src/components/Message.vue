<template>
  <div class="message">
    <p>Message content {{ message }}</p>
  </div>
</template>
<script>
export default {
  props: {
    message: {
      type: String,
      required: true,
    },
  },
};
</script>
<style lang="css" scoped>
.message {
  margin-top: 30px;
  font-size: 18px;
  font-style:italic;
  color: red;
}
</style>
