<script setup>
  import { computed } from 'vue';

  const props = defineProps(['courses']);
  

  const coursesDone = computed(() => {
    return props.courses.filter(course => course.done).length;
  })
</script>

<template>
  {{ `${coursesDone} cursos completos de um total de ${courses.length}`  }}
</template>

<style scoped>

</style>
