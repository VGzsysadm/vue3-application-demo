<script setup>
//Defining imports
import { ref, defineEmits } from 'vue';
//Defining events
const emits = defineEmits(['sort-items', 'order-items', 'favourite-items']);
//Defining variables & Props
const sortByItem = ref('');
const orderByItem = ref('');
const favouriteItem = ref(false);
//Defining Functions
const SortBy = () => {
  emits('sort-items', sortByItem.value);
}
const OrderBy = () => {
  emits('order-items', orderByItem.value);
}
const Favourite = ( ) => {
  emits('favourite-items', favouriteItem.value);
}
</script>

<template>
  <div class="filter-bar">
    <div class="filter-bar__select">
      <label for="sort">Sort by</label>
      <select v-model="sortByItem" @change="SortBy">
        <option value="name">Name</option>
        <option value="date">Date</option>
        <option value="family">Family</option>
        <option value="favourite">Favourite</option>
        <option value="rating">Rating</option>
      </select>
    </div>
    <div class="filter-bar__select">
      <label for="sort">Order by</label>
      <select v-model="orderByItem" @change="OrderBy">
        <option value="asc">Ascending</option>
        <option value="desc">Descending</option>
      </select>
    </div>
    <div class="filter-bar__check">
      <input type="checkbox" id="favorite" value=off v-model="favouriteItem" @change="Favourite"/>
      <label for="favorite">Favorite</label>
    </div>
  </div>
</template>
    
<style scoped>
.filter-bar {
display: flex;
align-items: center;
padding: 20px;
background-color: #f5f5f5;
border-bottom: 1px solid #ccc;
}
.filter-bar__select {
display: flex;
align-items: center;
margin-right: 20px;
}
.filter-bar__select label {
margin-right: 10px;
}
.filter-bar__select select {
padding: 10px;
border: 1px solid #ccc;
border-radius: 4px;
outline: none;
}
.filter-bar__check {
display: flex;
align-items: center;
}
.filter-bar__check input {
margin-right: 10px;
}
.filter-bar__check label {
cursor: pointer;
}
</style>
<script>
export default {
  name: 'Filter bar'
}
</script>