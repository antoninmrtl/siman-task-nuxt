<script setup>
const taches = useState('taches-globales', () => [])

onMounted(() => {
  let data = localStorage.getItem('mesTaches')
  if (data) {
    taches.value = JSON.parse(data)
  }
})

watch(
    taches, (nouvelleValeur) => {
      if (import.meta.client) {
        localStorage.setItem('mesTaches', JSON.stringify(nouvelleValeur))
      }
    },
    {deep: true},
)
</script>


<template>
  <NuxtPage />
</template>