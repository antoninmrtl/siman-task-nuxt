<script setup>
const route = useRoute()
const tacheId = route.params.id
</script>

<template>
  <UContainer class="py-10">
    <UCard>
      <h1>Détails de la tâche : {{ tacheId }}</h1>
      <UButton to="/" variant="link">Retour à la liste</UButton>
    </UCard>
  </UContainer>
</template>