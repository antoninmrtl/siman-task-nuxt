<script setup>
const nouvelleTache = ref('')
const itemsSelect = ref(['Basse', 'Normal', 'Haute'])
const value = ref('Basse')
const taches = useState('taches-globales', () => [])

function ajouterTache() {
  if (nouvelleTache.value.trim() !== '') {
    taches.value.push({
      texte: nouvelleTache.value.trim(),
      termine: false,
      priorite: value.value,
    })
  }
  nouvelleTache.value = ''
  value.value = 'Basse'
}

function supprimerTache(index) {
  taches.value.splice(index, 1)
}

const tachesRestantes = computed(() => {
  return taches.value.filter((tache) => tache.termine === false).length
})


</script>

<template>
  <UContainer class="max-w-xl py-10">
    <UCard>
      <h1>Siman-Task</h1>
      <hr/>
      <div class="flex gap-2 mb-6">
        <UInput class="w-full" v-model="nouvelleTache" />
        <USelect class="w-full" v-model="value" :options="itemsSelect"/>
        <UButton type="submit" @click="ajouterTache">Add Task</UButton>
      </div>
      <h3>Remining tasks : {{ tachesRestantes }}</h3>
      <ul class="space-y-3">
        <TacheItem
            v-for="(tache, index) in taches"
            :key="index"
            :tache="tache"
            :index="index"
            @supprimer="supprimerTache"
        />
      </ul>
    </UCard>
  </UContainer>
</template>

<style scoped>
.fait {
  text-decoration: line-through;
  color: gray;
}
</style>
