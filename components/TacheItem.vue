<script setup>
defineProps({
  tache: Object,
  index: Number
})

const emit = defineEmits(['supprimer'])
</script>

<template>
  <li class="flex items-center justify-between p-2 border rounded-lg border-gray-100 bg-gray-50/50">
    <div class="flex items-center gap-3">
      <UCheckbox v-model="tache.termine" />
      <NuxtLink :to="`/taches/${index}`" :class="{ 'line-through text-gray-400': tache.termine, 'hover:text-blue-500': true }">
        {{ tache.texte }}
      </NuxtLink>
    </div>

    <UButton color="red" variant="ghost" icon="i-heroicons-trash" @click="emit('supprimer', index)" />
  </li>
</template>