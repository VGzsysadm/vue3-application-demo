<script setup>
//Defining imports
import PlantItem from './PlantItem.vue';
//Defining events
const emits = defineEmits(['delete-plant'])
//Defining variables & Props
defineProps({
plantList: {
      type: Array,
      required: true
    }
})
//Defining Functions
const deletePlant = (id) => {
  emits('delete-plant', id);
}
</script>

<template>
  <div class="plant-list">
    <PlantItem v-for="(plant, index) in plantList" :key="index" :plant="plant" @delete-plant="deletePlant(plant.id)"/>
  </div>
</template>
    
<style scoped>
.plant-list {
  padding: 20px;
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-gap: 20px;
}
</style>
<script>
export default {
  name: 'Plant List'
}
</script>