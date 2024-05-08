<script setup>
//Defining imports
import { ref } from 'vue';
import { v4 as uuidv4 } from 'uuid';
import Swal from 'sweetalert2'
//Defining events
const emits = defineEmits(['add-plant'])
//Defining variables & Props
const formData = ref({
  name: '',
  description: '',
  image: '',
  date: '',
  family: '',
  genus: '',
  species: '',
  label: '',
  favourite: false,
  rating: 0,
  personalNote: ''
});
//Defining Functions
const createPlant = () => {
  if (!formData.value.name || !formData.value.description || !formData.value.image || !formData.value.date) {
    Swal.fire({
        icon: "error",
        title: "Oops...",
        text: "Please fill in all required fields.",
        footer: "The fields name, description, image and date are required."
        });
    return;
  }

  const labelsArray = formData.value.label.split(',').map(label => label.trim());

  const plant = {
    id: uuidv4(),
    name: formData.value.name,
    description: formData.value.description,
    image: formData.value.image,
    date: formData.value.date,
    family: formData.value.family,
    genus: formData.value.genus,
    species: formData.value.species,
    label: labelsArray,
    favourite: formData.value.favourite,
    rating: formData.value.rating,
    personalNote: formData.value.personalNote
  };

  emits('add-plant', plant);

  clearForm();
};
const clearForm = () => {
  formData.value = {
    name: '',
    description: '',
    image: '',
    date: '',
    family: '',
    genus: '',
    species: '',
    label: '',
    favourite: false,
    rating: 0,
    personalNote: ''
  };
};
</script>

<template>
    <div class="plant-form">
        <form class="plant-form__form" @submit.prevent="createPlant">
            <div class="plant-form__form-group">
                <label for="name">Name*:</label>
                <input type="text" id="name" name="name" v-model="formData.name">
            </div>
            <div class="plant-form__form-group">
                <label for="description">Description*</label>
                <input type="text" id="description" name="description" v-model="formData.description">
            </div>
            <div class="plant-form__form-group">
                <label for="image">Image URL:*</label>
                <input type="text" id="image" name="image" v-model="formData.image">
            </div>
            <div class="plant-form__form-group">
                <label for="date">Date:*</label>
                <input type="date" id="date" name="date" v-model="formData.date">
            </div>
            <div class="plant-form__form-group">
                <label for="family">Family:</label>
                <input type="string" id="family" name="family" v-model="formData.family">
            </div>
            <div class="plant-form__form-group">
                <label for="genus">Genus:</label>
                <input type="text" id="genus" name="genus" v-model="formData.genus">
            </div>
            <div class="plant-form__form-group">
                <label for="species">Species:</label>
                <input type="text" id="species" name="species" v-model="formData.species">
            </div>
            <div class="plant-form__form-group">
                <label for="label">Labels:<small>(Separated by comas)</small></label>
                <input type="text" id="label" name="label" v-model="formData.label">
            </div>
            <div class="plant-form__form-group">
                <label for="favourite">Favourite:</label>
                <input type="checkbox" id="favourite" name="favourite" v-model="formData.favourite">
            </div>
            <div class="plant-form__form-group">
                <label for="rating">Rating:</label>
                <input type="range" id="rating" name="rating" min="0" max="5" v-model="formData.rating">
            </div>
            <div class="plant-form__form-group">
                <label for="personalNote">Personal Note:</label>
                <textarea id="personalNote" name="personalNote" rows="5" cols="30" v-model="formData.personalNote"></textarea>
            </div>
            <div class="plant-form__form-group plant-form__form-group--actions">
                <button class="plant-form__submit">Create</button>
            </div>
        </form>
    </div>
</template>
    
<style scoped>
.plant-form {
padding: 1rem;
}
.plant-form__form {
display: grid;
grid-template-columns: 1fr 1fr;
gap: 1rem;
@media (max-width: 768px) {
    grid-template-columns: 1fr;
}
}
.plant-form__form-group {
display: flex;
flex-direction: column;
}
.plant-form__form-group label {
margin-bottom: 0.5rem;
}
.plant-form__form-group input,
.plant-form__form-group textarea {
padding: 0.5rem;
border: 1px solid #ccc;
border-radius: 0.25rem;
}
.plant-form__form-group input[type="checkbox"] {
width: auto;
}
.plant-form__form-group input[type="range"] {
width: 100%;
}
.plant-form__form-group--actions {
grid-column: 1 / -1;
}
.plant-form__submit {
padding: 0.5rem;
background-color: #007bff;
color: white;
border: none;
border-radius: 0.25rem;
cursor: pointer;
}
</style>
<script>
export default {
  name: 'Plant Form'
}
</script>