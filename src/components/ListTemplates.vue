<template>
  <div class="list_templates">
    <button @click="plovRecipe" class="plov_template">Plov recipe</button>
    <button @click="antonQuote" class="anton">Anton's quote</button>
    <button @click="dailyList" class="regular_template">Daily list</button>
  </div>
</template>

<script>
export default {
  methods: {
    antonQuote() {
      this.$emit('anton-quote');
    },
    plovRecipe() {
      this.$emit('plov-recipe');
    },
    dailyList() {
      this.$emit('daily-list');                   /*Emits for filling parents array*/
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

.list_templates {
  grid-area: 1 / 1 / 2 / 4;
}

.list_templates button {
  width: calc(100% / 3);
}
</style>