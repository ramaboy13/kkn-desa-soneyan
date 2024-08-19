<script setup>
import { onMounted, ref } from 'vue'

const recipes = ref([])
const displayedRecipes = ref(6) // Jumlah resep yang ditampilkan pertama kali
const selectedRecipe = ref(null)
const showModal = ref(false)

onMounted(async () => {
  try {
    const response = await fetch('/src/assets/data.json')
    const data = await response.json()
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
  displayedRecipes.value = 6 // Kembalikan jumlah resep yang ditampilkan ke 6
}
</script>

<template>
  <main>
    <!--Home Section-->
    <section class="py-5 min-vh-100 d-flex align-items-center position-relative">
      <div class="container">
        <div class="row justify-content-center">
          <div class="col-lg-7">
            <div class="text-center">
              <h1 class="display-3 fw-bold">
                For Quick Designing, there is
                <span class="text-primary">Bootstrap</span>
              </h1>
              <p class="lead py-3 py-md-4">
                Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nam feugiat erat quis
                pulvinar consectetur adipiscing elit semper.
              </p>
              <a
                class="mx-auto bg-primary text-white d-flex align-items-center justify-content-center rounded-circle"
                href=""
                style="width: 60px; height: 60px"
                ><svg
                  class="bi bi-play-fill"
                  fill="currentColor"
                  height="24"
                  viewbox="0 0 16 16"
                  width="24"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    d="m11.596 8.697-6.363 3.692c-.54.313-1.233-.066-1.233-.697V4.308c0-.63.692-1.01 1.233-.696l6.363 3.692a.802.802 0 0 1 0 1.393z"
                  ></path></svg
              ></a>
            </div>
          </div>
        </div>
        <a
          class="position-absolute bottom-0 start-50 translate-middle text-primary"
          href="#scrollToContent"
          ><svg
            class="bi bi-arrow-down"
            fill="currentColor"
            height="32"
            viewbox="0 0 16 16"
            width="32"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M8 1a.5.5 0 0 1 .5.5v11.793l3.146-3.147a.5.5 0 0 1 .708.708l-4 4a.5.5 0 0 1-.708 0l-4-4a.5.5 0 0 1 .708-.708L7.5 13.293V1.5A.5.5 0 0 1 8 1z"
              fill-rule="evenodd"
            ></path></svg
        ></a>
      </div>
    </section>

    <section class="py-5">
      <div class="container">
        <div class="row justify-content-center text-center mb-4 mb-md-5">
          <div class="col-xl-9 col-xxl-8">
            <span class="text-muted">Read More</span>
            <h2 class="display-5 fw-bold">Our Blog</h2>
            <p class="lead">
              Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor
              incididunt ut labore et dolore magna aliqua
            </p>
          </div>
        </div>
        <div class="row gy-4">
          <div
            class="col-md-4"
            v-for="recipe in recipes.slice(0, displayedRecipes)"
            :key="recipe.recipe_name"
            @click="openModal(recipe)"
          >
            <div class="shadow p-4">
              <img src="" :alt="recipe.recipe_name" class="recipe-image" />
              <div class="text-muted">10.10.2017</div>
              <h2 class="fw-semibold text-primary mt-1">
                {{ recipe.recipe_name }}
              </h2>
              <p class="mt-3">
                Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vestibulum congue risus sit
                amet dictum malesuada. Vestibulum viverra iaculis turpis, vitae varius lectus
                imperdiet at. Sed ultrices, ante vitae maximus laoreet, magna quam tincidunt ex, non
                faucibus justo dui commodo libero.
              </p>
            </div>
          </div>
        </div>

        <div class="col-md-2 d-grid mx-auto mt-5">
          <button
            v-if="displayedRecipes < recipes.length"
            @click="showMore"
            class="btn btn-primary btn-lg"
          >
            Show More
          </button>

          <button v-else @click="showLess" class="btn btn-primary btn-lg">Show Less</button>
        </div>

        <div v-if="showModal" class="modal">
          <div class="modal-content">
            <span class="close" @click="closeModal">&times;</span>
            <h2>{{ selectedRecipe.recipe_name }}</h2>
            <div class="ingredients">
              <strong>Bahan-bahan:</strong>
              <ul>
                <li v-for="ingredient in selectedRecipe.ingredients" :key="ingredient.ingredient">
                  {{ ingredient.ingredient }}: {{ ingredient.quantity }}
                </li>
              </ul>
            </div>
            <div class="instructions">
              <strong>Cara memasak:</strong>
              <p>{{ selectedRecipe.instructions }}</p>
            </div>
          </div>
        </div>
      </div>
    </section>
  </main>
</template>

<style scoped>
* {
  font-family: 'inter', sans-serif;
  scroll-behavior: smooth;
}
.recipe-list {
  display: flex;
  flex-wrap: wrap;
}

.recipe-card {
  border: 1px solid #ddd;
  border-radius: 8px;
  margin: 10px;
  padding: 10px;
  cursor: pointer;
  width: 200px;
  text-align: center;
}

.recipe-image {
  width: 100%;
  height: auto;
  border-radius: 8px;
}

.recipe-title {
  font-weight: bold;
  margin-top: 10px;
}

button {
  margin-top: 20px;
  padding: 10px 20px;
  background-color: #42b983;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #358a63;
}

.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background-color: rgb(24, 24, 24);
  padding: 20px;
  border-radius: 8px;
  width: 80%;
  max-width: 600px;
  position: relative;
}

.close {
  position: absolute;
  top: 10px;
  right: 20px;
  font-size: 24px;
  cursor: pointer;
}
</style>
