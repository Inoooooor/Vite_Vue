<template>
  <div class="list_templates">
    <button @click="plovRecipe" class="plov_template">Plov recipe</button>
    <button @click="antonQuote" class="anton">Anton's quote</button>
    <button @click="dailyList" class="regular_template">Daily list</button>
  </div>
</template>

<script>
export default {
  props: {
    array: Array,
  },
  data() {
    return {
      count: 0
    }
  },
  methods: {
    antonQuote() {
      this.$emit('anton-quote');
    },
    plovRecipe() {
      this.$emit('plov-recipe');
    },
    dailyList() {
      this.$emit('daily-list');
    },
  }
}
</script>
<style scoped>
button {
  font-size: 0.7em;
  font-weight: bold;
  flex-grow: 1;
}
</style>