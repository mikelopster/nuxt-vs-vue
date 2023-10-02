<script setup>
const route = useRoute()

console.log(route.params.id)
</script>

<template>
  <div>{{ $route.params.id }}</div>
</template>