<script setup>
const nouvelleTache = ref('')
const itemsSelect = ref(['Basse', 'Normal', 'Haute'])
const value = ref('Basse')
const taches = useState('taches-globales', () => [])
const filtreActuel = ref('Toutes')
const erreurSaisie = ref('')

function ajouterTache() {
  if (nouvelleTache.value.trim() !== '' && nouvelleTache.value.length >= 3) {
    taches.value.push({
      texte: nouvelleTache.value.trim(),
      termine: false,
      priorite: value.value,
    })
    erreurSaisie.value= ''
  }else {
    erreurSaisie.value = 'Une tâche ne peut-être vide ou doit être au moins de 3 caractères'
  }
  nouvelleTache.value = ''
  value.value = 'Basse'
}

function supprimerTache(indexDansFiltre) {
  const tacheASupprimer = tachesFiltrees.value[indexDansFiltre]
  const indexReel = taches.value.indexOf(tacheASupprimer)
  if (indexReel !== -1) {
    taches.value.splice(indexReel, 1)
  }
}

const tachesRestantes = computed(() => {
  return taches.value.filter((tache) => tache.termine === false).length
})

const tachesFiltrees = computed(() => {
  if (filtreActuel.value === 'À faire') {
    return taches.value.filter(tache => !tache.termine)
  }
  if (filtreActuel.value === 'Terminées') {
    return taches.value.filter(tache => tache.termine)
  }
  return taches.value
})
</script>

<template>
  <UContainer class="max-w-xl py-10">
    <UCard>
      <h1>Siman-Task</h1>
      <hr/>
      <div>
        <UButtonGroup class="flex mb-4">
          <UButton @click="filtreActuel = 'Toutes'" :color="filtreActuel === 'Toutes' ? 'primary' : 'gray'">Toutes</UButton>
          <UButton @click="filtreActuel = 'À faire'" :color="filtreActuel === 'À faire' ? 'primary' : 'gray'">À faire</UButton>
          <UButton @click="filtreActuel = 'Terminées'" :color="filtreActuel === 'Terminées' ? 'primary' : 'gray'">Terminées</UButton>
        </UButtonGroup>
      </div>
      <div class="flex gap-2 mb-6">
        <UInput class="w-full" v-model="nouvelleTache" />
        <USelect class="w-full" v-model="value" :options="itemsSelect"/>
        <UButton type="submit" @click="ajouterTache">Add Task</UButton>
      </div>
      <h3 class="text-red-500">{{erreurSaisie}}</h3>
      <h3>Remining tasks : {{ tachesRestantes }}</h3>
      <ul class="space-y-3">
        <TacheItem
            v-for="(tache, index) in tachesFiltrees"
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
