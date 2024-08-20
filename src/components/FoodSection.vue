<script setup>
import { onMounted, ref } from 'vue'
import data from '../assets/data.json'

const dataFood = data
const recipes = ref([])
const selectedRecipe = ref(null)
const showModal = ref(false)
const initialDisplayCount = ref(3) // Jumlah awal resep yang ditampilkan
const displayedRecipes = ref(initialDisplayCount.value)

onMounted(async () => {
  try {
    // const response = await fetch('/src/assets/data.json')
    const data = dataFood
    recipes.value = data.recipes
  } catch (error) {
    console.error('Error fetching recipes:', error)
  }
})

function openModal(recipe) {
  selectedRecipe.value = recipe
  showModal.value = true
}

function closeModal() {
  showModal.value = false
}

function showMore() {
  displayedRecipes.value = recipes.value.length // Tampilkan semua resep
}

function showLess() {
  displayedRecipes.value = initialDisplayCount.value // Kembali ke jumlah awal resep yang ditampilkan
}
</script>

<template>
  <section class="" id="makanansehat">
    <div class="container">
      <div class="row justify-content-center text-center mb-4 mb-md-5">
        <div class="col-xl-9 col-xxl-8" data-aos="fade-down">
          <span style="color: #349d63">Rekomendasi</span>
          <h2 class="display-5 fw-bold">Menu Makanan<span style="color: #349d63"> Sehat</span></h2>
          <p class="lead">
            Berikut ini kami rekomendasikan menu makanan dari posyandu yang efektif mencegah
            stunting. Setiap menu dilengkapi bahan-bahan dan cara memasaknya agar mudah
            dipraktikkan.
          </p>
        </div>
      </div>
      <div class="row g-5" data-aos="fade-up">
        <div
          class="col-md-4"
          v-for="recipe in recipes.slice(0, displayedRecipes)"
          :key="recipe.recipe_name"
          @click="openModal(recipe)"
        >
          <a href="javascript:void(0)" class="text-decoration-none">
            <div class="card border-0 bg-light-subtle shadow-lg">
              <img
                :src="recipe.image"
                :alt="recipe.recipe_name"
                class="img-cover rounded-top-2"
                style="width: 100%; height: 300px"
              />
              <div class="card-body p-0 text-center mt-4">
                <h5 class="text-dark text-decoration-none fw-bolder">
                  {{ recipe.recipe_name }}
                </h5>
                <p class="mt-3" style="color: #349d63">Lihat resep menu selengkapnya -></p>
              </div>
            </div>
          </a>
        </div>
      </div>
      <div class="text-center mt-4">
        <button v-if="displayedRecipes < recipes.length" class="btn button" @click="showMore">
          Show More
        </button>
        <button
          v-if="displayedRecipes > initialDisplayCount"
          class="btn button ms-2"
          @click="showLess"
        >
          Show Less
        </button>
      </div>
    </div>

    <!-- Modal -->
    <div v-if="showModal" class="modal" tabindex="-1" style="display: block">
      <div class="modal-dialog modal-dialog-centered modal-dialog-scrollable">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title">{{ selectedRecipe.recipe_name }}</h5>
            <button type="button" class="btn-close" aria-label="Close" @click="closeModal"></button>
          </div>
          <div class="modal-body">
            <div class="ingredients">
              <strong>Bahan-bahan:</strong>
              <ul>
                <li v-for="ingredient in selectedRecipe.ingredients" :key="ingredient.ingredient">
                  {{ ingredient.ingredient }}: {{ ingredient.quantity }}
                </li>
              </ul>
            </div>
            <div class="instructions mt-3">
              <strong>Cara memasak:</strong>
              <p>{{ selectedRecipe.instructions }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
