<script setup>
const route = useRoute()
const tacheId = route.params.id
const itemsSelect = ref(['Basse', 'Normal', 'Haute'])
const value = ref('Basse')
const taches = useState('taches-globales', () => [])
const laTache = computed(() => taches.value[route.params.id])
</script>

<template>
  <UContainer class="py-10">
    <UCard v-if="laTache">
      <h1>Détails de la tâche : {{ tacheId }}</h1>
      <div>
        <UFormGroup label="Modifier la tâche" class="mb-4 mt-3">

          <div class="flex justify-center gap-5">
            <UInput class="w-full" v-model="laTache.texte"/>
            <USelect class="w-full" v-model="laTache.priorite" :options="itemsSelect"/>
          </div>
        </UFormGroup>

        <div class="flex gap-5 p-5">
          <h2>{{ laTache ? laTache.texte : 'Tâche introuvable' }}</h2>
          <UBadge
              :class="{'bg-red-500 text-white' : laTache.priorite == 'Haute', 'bg-blue-500' : laTache.priorite == 'Normal'}">
            {{ laTache.priorite }}
          </UBadge>
        </div>
      </div>
      <UButton to="/" variant="link">Sauvegarder</UButton>
    </UCard>
  </UContainer>
</template>