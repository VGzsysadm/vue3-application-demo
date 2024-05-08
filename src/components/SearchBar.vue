<script setup>
//Defining imports
import { ref } from 'vue';
//Defining events
const emits = defineEmits(['show-form', 'sesarch', 'reset-clear']);
//Defining variables & Props
const searchText = ref('');
//Defining Functions
const showForm = () => {
  emits('show-form');
}
const clearSearch = () => {
  searchText.value = '';
  emits('reset-clear');
}
const search = () => {
  emits('sesarch', searchText.value);
}
</script>

<template>
  <div class="search-bar">
    <input type="text" id="plant" name="plant" v-model="searchText" @input="search" placeholder="Search plant"><br><br>
    <button class="clear" @click="clearSearch">Clear</button>
    <button class="add"@click="showForm()">Add Plant</button>
  </div>
</template>
    
<style scoped>
.search-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 20px;
  background-color: #f5f5f5;
  border-bottom: 1px solid #e5e5e5;
}
.search-bar input {
  width: 100%;
  padding: 10px;
  border: 1px solid #e5e5e5;
  border-radius: 4px;
  outline: none;
}
.search-bar button {
  padding: 10px;
  border: 1px solid #e5e5e5;
  border-radius: 4px;
  outline: none;
  cursor: pointer;
  min-width: 100px;
}
.search-bar .clear {
  margin-right: 10px;
}
.search-bar .add {
  background-color: #007bff;
  color: #fff;
}
</style>
<script>
export default {
  name: 'Search bar'
}
</script>