<script setup>
const nouvelleTache = ref('')
const taches = ref([])

function ajouterTache() {
  if (nouvelleTache.value.trim() !== '') {
    taches.value.push({
      texte: nouvelleTache.value.trim(),
      termine: false,
    })
  }
  nouvelleTache.value = ''
}

function supprimerTache(index) {
  taches.value.splice(index, 1)
}

const tachesRestantes = computed(() => {
  return taches.value.filter((tache) => tache.termine === false).length
})

onMounted(() => {
  let data = localStorage.getItem('mesTaches')
  if (data) {
    taches.value = JSON.parse(data)
  }
})

watch(
    taches, (nouvelleValeur) => {
      localStorage.setItem('mesTaches', JSON.stringify(nouvelleValeur))
    },
    {deep: true},
)
</script>

<template>
  <UContainer class="max-w-xl py-10">
    <UCard>
      <h1>Siman-Task</h1>
      <hr/>
      <div class="flex gap-2 mb-6">
        <UInput class="w-full" v-model="nouvelleTache"/>
        <UButton type="submit" @click="ajouterTache">Add Task</UButton>
      </div>
      <h3>Remining tasks : {{ tachesRestantes }}</h3>
      <ul class="list-none p-0">>
        <li class="flex items-center justify-between mb-3" v-for="(tache, index) in taches" :key="index">
          <div class="flex items-center gap-3">
            <UCheckbox v-model="tache.termine" />
            <span :class="{ fait: tache.termine }">{{ tache.texte }}</span>
          </div>
          <UButton type="submit" @click="supprimerTache(index)">Delete task</UButton>
        </li>
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
