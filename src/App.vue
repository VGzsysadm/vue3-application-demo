<script setup>
//Defining imports
import { ref, computed } from 'vue';
import PlantList from './components/PlantList.vue';
import SearchBar from './components/SearchBar.vue';
import Filterbar from './components/Filterbar.vue';
import ModalLayer from './components/ModalLayer.vue';
import PlantForm from './components/PlantForm.vue';
import Swal from 'sweetalert2'
//Defining variables & Props
const plantItems = ref([
  { id: 1, name: 'Monstera Deliciosa', description: "Monstera Deliciosa, also known as 'Adam's Rib', is a popular houseplant for its large perforated leaves and easy care. This plant is fantastic for its exotic look and how easy it is to maintain.", image: 'https://cdn.webshopapp.com/shops/30495/files/447582333/monstera-deliciosa-hoja-de-ventana-maceta-21cm-alt.jpg', date: "2023-05-15",  family: "Araceae", genus: "Monstera", species: "Deliciosa", label: ['easy care', 'inside', "resistant"], favourite:true, featured: true, rating: "4", personalNote: "I love this plant for its exotic look and how easy it is to maintain."},
  { id: 2, name: 'Ficus Elastica', description: "The Ficus Elastica, or 'Rubber Leaf Fig', is an indoor tree known for its large, glossy leaves. It is a resistant plant and easy to care for.", image: 'https://www.mygarden.com.co/wp-content/uploads/2020/05/PLANTA-FICUS-ELASTICA-ROBUSTA-1-.jpg', date: "2022-11-20",  family: "Moraceae", genus: "Ficus", species: "Elastica", label: ["inside", "resistant", "easy care"], favourite:false, rating: "5", personalNote: "I have a Ficus Elastica in my living room and it always gets a lot of compliments on its beautiful leaves."},
  { id: 3, name: 'Sansevieria Trifasciata', description: "Sansevieria Trifasciata, also known as 'Mother-in-Law's Tongue', is a succulent plant popular for its elegant appearance and its ability to purify the air.", image: 'https://foliahouse.com.au/cdn/shop/products/Sansevieria-Trifasciata-Laurentii---17cm-Pot-Folia-House-1678164530_720x.jpg', date: "2023-03-10",  family: "Asparagaceae", genus: "Sansevieria", species: "Trifasciata", label: ["inside", "purifying", "resistant"], favourite:false, rating: "4", personalNote: "Sansevieria is one of my favorite houseplants. In addition to being beautiful, it is easy to care for and helps keep the air in my home clean."},
  { id: 4, name: 'Pothos', description: "Pothos is an indoor climbing plant prized for its glossy leaves and ability to grow in low light conditions. It is perfect for gardening beginners.", image: 'https://media.houseandgarden.co.uk/photos/64bff5f4d6a55acd0397054e/master/pass/Screenshot%202023-07-25%20at%2017.17.10.png', date: "2023-08-25",  family: "Araceae", genus: "Epipremnum", species: "Aureum", label: ["inside", "easy care", "low light"], favourite:false, rating: "4", personalNote: "Pothos was my first houseplant and is still one of my favorites. It grows fast and is very resistant."},
  { id: 5, name: 'Calathea Orbifolia', description: "Calathea Orbifolia is a houseplant with large, round leaves, with a unique pattern in shades of green and silver. It is known for its elegance and its ability to close its leaves at night.", image: 'https://cdn.webshopapp.com/shops/30495/files/447589171/calathea-orbifolia-calathea-orbifolia-cesta-marant.jpg', date: "2024-01-05",  family: "Marantaceae", genus: "Calathea", species: "Orbifolia", label: ["inside", "decorative", "humidity"], favourite:false, rating: "4", personalNote: "Calathea Orbifolia is a beauty in my living room. I love watching its leaves open and close during the day and night."},
  ]);
const showModal = ref(false);
const searchTerm = ref('');
const sortBy = ref('');
const orderBy = ref('');
const favouriteItems = ref(false);
//Defining Functions
const addPlant = (plant) => {
  plantItems.value.push(plant);
  Swal.fire({
    position: "top-end",
    icon: "success",
    title: "The plant " + plant.name + " has been created.",
    showConfirmButton: false,
    timer: 3500
  });
  toggleForm();
};
const deletePlant = (id) => {
  const index = plantItems.value.findIndex(plant => plant.id === id);
  if (index !== -1) {
    Swal.fire({
      title: "Are you sure?",
      text: "Do you want to delete the plant " + plantItems.value[index].name + " ?",
      icon: "warning",
      showCancelButton: true,
      confirmButtonColor: "#3085d6",
      cancelButtonColor: "#d33",
      confirmButtonText: "Yes, delete it!"
    }).then((result) => {
      if (result.isConfirmed) {
        Swal.fire({
          title: "Deleted!",
          text: "The Plant " + plantItems.value[index].name + " has been deleted",
          icon: "success"
        });
        plantItems.value.splice(index, 1);
      }
    });
    
  }
};
const toggleForm = () => {
  showModal.value = !showModal.value;
};
const setSearchTerm = (searchText) => {
  searchTerm.value = searchText;
};

const sortItems = (sort) => {
  sortBy.value = sort;
};

const orderItems = (order) => {
  orderBy.value = order;
};
const favouriteItemsToggle = () => {
  favouriteItems.value = !favouriteItems.value;
};
const plantListFiltered = computed(() => {

  let filteredList = plantItems.value.filter(plant => {
    const matchesName = plant.name.toLowerCase().includes(searchTerm.value.toLowerCase());
    const matchesDescription = plant.description.toLowerCase().includes(searchTerm.value.toLowerCase());
    const matchesFamily = plant.family.toLowerCase().includes(searchTerm.value.toLowerCase());
    const matchesGenus = plant.genus.toLowerCase().includes(searchTerm.value.toLowerCase());
    const matchesSpecies = plant.species.toLowerCase().includes(searchTerm.value.toLowerCase());
    const matchesLabel = plant.label.some(label => label.toLowerCase().includes(searchTerm.value.toLowerCase()));

    return searchTerm.value === '' || matchesName || matchesDescription || matchesFamily || matchesGenus || matchesSpecies || matchesLabel;
});

  if (favouriteItems.value) {
    filteredList = filteredList.filter(plant => plant.favourite);
  }

  if (sortBy.value === 'name') {
    filteredList.sort((a, b) => {
      return a.name.localeCompare(b.name);
    });
  } else if (sortBy.value === 'date') {
    filteredList.sort((a, b) => {
      const dateA = new Date(a.date);
      const dateB = new Date(b.date);
      return dateB - dateA;
    });
  } else if (sortBy.value === 'family') {
    filteredList.sort((a, b) => {
      return a.family.localeCompare(b.family);
    })
  } else if (sortBy.value === 'favourite') {
    filteredList.sort((a, b) => {
        return b.favourite - a.favourite;
    });
  } else if (sortBy.value === 'rating') {
    filteredList.sort((a, b) => {
      return b.rating.localeCompare(a.rating)
    });
  }
  
  if (orderBy.value === 'desc') {
    filteredList.reverse();
  }

  return filteredList;
});

const resetClear = () => {
  searchTerm.value = '';
};
</script>

<template>
    <header class="header">
      <div class="header__left">
        <img class="logo" src="/assets/logo.png" alt="Logo">
        <h1 class="title">Plants database </h1>
      </div>
    </header>
      <SearchBar @show-form="toggleForm" @sesarch="setSearchTerm" @reset-clear="resetClear"/>
      <Filterbar @sort-items="sortItems" @order-items="orderItems" @favourite-items="favouriteItemsToggle"/>
      <main class="main">
        <PlantList :plantList="plantListFiltered" @delete-plant="(id) => deletePlant(id)"/>
      </main>
      <ModalLayer v-if="showModal" @close-modal="toggleForm">
        <template #header>
          <h2>Add new plant</h2>
        </template>
        <template v-slot:body>
            <PlantForm @add-plant="addPlant"/>
        </template>
      </ModalLayer>
</template>

<style>
body {
  padding: 0;
  margin: 0;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 20px;
  background-color: #f5f5f5;
  border-bottom: 1px solid #e5e5e5;
}

.header__left {
  display: flex;
  align-items: center;
}

.logo {
  height: 40px;
  margin-right: 10px;
}

.title {
  font-size: 24px;
  font-weight: 400;
}
</style>
