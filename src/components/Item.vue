<template>
  <li class="card" @click="$emit('change')">
    <h2 class="card-title">{{ item.name }}</h2>
    <template v-for="(value, name, index) in item">
      <p class="card-text" :key="name" v-if="index < 5">
        {{ name }}: {{ value }}
      </p>
    </template>
  </li>
</template>

<script>
export default {
  name: "Item",
  props: {
    item: Object,
  },
};
</script>

<style scoped>
.card {
  border: 2px solid #4fc08d;
  border-radius: 4px;
  cursor: pointer;
  padding: 15px;
  flex: 1;
}
</style>
