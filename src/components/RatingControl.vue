<template>
  <ul >
    <li v-for="(rating, key) in ratings" :key="key" :class="{ selected: modelValue === key}">
      <button type="button" @click="selectRating(key)">{{  rating }}</button>
    </li>
  </ul>
</template>

<script>
export default {
  props: ['modelValue'],                    // special Vue prop for v-model
  emits: ['update:modelValue'],        // special Vue event for v-model
  data() {
    return {
      ratings: {
        poor: 'Poor',
        average: 'Average',
        great: 'Great'
      }
    }
  },
  methods: {
    selectRating(rating) {
      this.$emit('update:modelValue', rating)
    }
  },
}
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0.5rem 0;
  padding: 0;
  display: flex;
}

li {
  margin: 0 1rem;
  border: 1px solid #ccc;
  padding: 1rem;
  display: flex;
  justify-content: center;
  align-items: center;
}

button {
  font: inherit;
  border: none;
  background-color: transparent;
  cursor: pointer;
}

.selected {
  border-color: #bd70db;
}

.selected button {
  color: #bd70db;
}
</style>