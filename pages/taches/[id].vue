<script setup>
const route = useRoute()
const tacheId = route.params.id
const taches = useState('taches-globales', () => [])
const laTache = computed(() => taches.value[route.params.id])
</script>

<template>
  <UContainer class="py-10">
    <UCard>
      <h1>Détails de la tâche : {{ tacheId }}</h1>
      <h2>{{ laTache ? laTache.texte : 'Tâche introuvable' }}</h2>
      <UButton to="/" variant="link">Retour à la liste</UButton>
    </UCard>
  </UContainer>
</template>