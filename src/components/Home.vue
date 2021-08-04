<template>
  <div>
    <h1 class="mt-3 mb-3">Trade or view your Portfolio</h1>
    <h6>You may save & load your data</h6>
    <h6>Click on 'End Day' to begin a New Day!</h6>
    <hr />
    <p>Your funds: {{ funds | currency }}</p>
  </div>
</template>

<script>
export default {
  computed: {
    funds() {
      return this.$store.getters.funds;
    },
  },
};
</script>
