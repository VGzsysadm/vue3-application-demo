<script setup>
//Defining events
const emits = defineEmits(['delete-plant'])
//Defining variables & Props
defineProps({
  plant: {
      type: Object,
      required: true,
      properties: {
        id: {
          type: Number,
          required: true,
        },
        name: {
          type: String,
          required: true,
        },
        description: {
          type: String,
          required: true,
        },
        image: {
          type: String,
          required: true,
        },
        date: {
          type: Date,
          required: true,
        },
        family: {
          type: String,
          required: true,
        },
        genus: {
          type: String,
          required: true,
        },
        species: {
          type: String,
          required: true,
        },
        label: {
          type: Array,
          required: true,
        },
        favourite: {
          type: Boolean,
          required: true,
        },
        rating: {
          type: Number,
          required: true,
          validator: (value, prop) => {
            return [prop >= 1 && prop <= 5].includes(value)
        }},
        personalNote: {
          type: String,
          required: true,
        }
      }
}})
//Defining Functions
const deletePlant = (id) => {
  emits('delete-plant', id);
}
</script>

<template>
    <div class="plant-item" :class="{ 'plant-item--favourite': plant.favourite }">
      <button class="plant-item__delete" @click="deletePlant(plant.id)">
        <img src="/assets/delete-button.svg" alt="Delete plant">
      </button>
      <div class="plant-item__image">
        <img :src='plant.image' alt="Plant Image">
      </div>
      <div class="plant-item__info">
          <h2 class="plant-item__title">{{ plant.name }}</h2>
          <div class="plant-item__data">
            <p class="plant-item__date">Date: {{ plant.date }}</p>
            <p class="plan-item__family">Family: {{ plant.family }}</p>
            <p class="plant-item__genus">Genus: {{ plant.genus }}</p>
            <p class="plant-item__especies">Species: {{ plant.species }}</p>
          </div>
          <p class="plant-item__description">{{ plant.description }}</p>
          <p class="plant-item__personal-note"> {{ plant.personalNote }}</p>
          <div class="plant-item__extra">
            <p class="plant-item__rating">{{ plant.rating }}/5</p>
            <p class="plant-item__labels"><span v-for="(label, index) in plant.label" :key="index">{{ label }}</span></p>
          </div>
      </div>
    </div>
</template>
    
<style scoped>
.plant-item {
display: flex;
padding: 1rem;
border: 1px solid #ccc;
border-radius: 0.5rem;
margin-bottom: 1rem;
position: relative;
}
.plant-item--favourite {
background-color: #f0f0f0;
}
.plant-item__delete {
background-color: transparent;
border: none;
padding: 10px;
cursor: pointer;
position: absolute;
top: 0;
right: 0;
}
.plant-item__delete img {
width: 20px;
}
.plant-item__image {
margin-right: 1rem;
}
.plant-item__image img {
width: 200px;
height: 200px;
object-fit: cover;
border-radius: 0.5rem;
}
.plant-item__info {
  flex: 1;
}
.plant-item__title {
margin: 0;
font-size: 1.5rem;
margin-bottom: 1rem;
border-bottom: 1px solid #ccc;
}
.plant-item__description {
margin: 0 0 1rem;
}
.plant-item__data {
margin-bottom: 1rem;
border-bottom: 1px solid #ccc;
padding-bottom: 1rem;
}
.plant-item__data p {
margin: 0;
}
.plant-item__personal-note {
margin: 0 0 1rem;
}
.plant-item__extra {
display: flex;
justify-content: space-between;
}
.plant-item__rating {
margin: 0;
}
.plant-item__labels {
margin: 0;
}
.plant-item__labels span {
margin-right: 0.5rem;
padding: 0.25rem 0.5rem;
border: 1px solid #ccc;
border-radius: 0.25rem;
background-color: #f0f0f0;
}
</style>
<script>
export default {
  name: 'Plant Item'
}
</script>