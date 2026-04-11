<script setup>
import { ref, computed, onMounted, watch } from 'vue'
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
    { deep: true },
)
</script>

<template>
  <main>
    <h1>Siman-Task</h1>
    <hr />
    <input v-model="nouvelleTache" type="text" />
    <button type="submit" @click="ajouterTache">Add Task</button>
    <h3>Remining tasks : {{ tachesRestantes }}</h3>
    <ul>
      <li v-for="(tache, index) in taches" :key="index">
        <input type="checkbox" v-model="tache.termine" />
        <span :class="{ fait: tache.termine }">{{ tache.texte }}</span>
        <button type="submit" @click="supprimerTache(index)">Delete task</button>
      </li>
    </ul>
  </main>
</template>

<style scoped>
.fait {
  text-decoration: line-through;
  color: gray;
}
</style>
