<script setup>
import { onMounted, ref } from 'vue'

const recipes = ref([])
const selectedRecipe = ref(null)
const showModal = ref(false)
const initialDisplayCount = ref(3) // Jumlah awal resep yang ditampilkan
const displayedRecipes = ref(initialDisplayCount.value)

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
  displayedRecipes.value = initialDisplayCount.value // Kembali ke jumlah awal resep yang ditampilkan
}
</script>

<template>
  <main>
    <!--Home Section-->
    <section class="py-5 home">
      <div class="container">
        <div class="row align-items-center mt-3">
          <div class="col-lg-6 mb-4 mb-lg-0" data-aos="fade-right">
            <h4 class="display-3 fw-bold">
              Halo, selamat datang di <span class="main-span">Healthy Food</span>
            </h4>
            <p class="lead my-3">
              Kami menawarkan berbagai rekomendasi makanan sehat yang efektif dalam mencegah
              stunting, rekomendasi dirancang dengan cermat oleh Posyandu dan ahli gizi.
            </p>
            <a class="btn btn-lg button mt-2" href="#tentangkami">Selengkapnya</a>
          </div>
          <div class="col-lg-6" data-aos="fade-left">
            <img alt="" class="main-image img-fluid" src="../public/img/makanan.png" />
          </div>
        </div>
      </div>
    </section>

    <!--Section Tentang Kami-->
    <section class="py-5 mt-5" id="tentangkami">
      <div class="container">
        <div class="row align-items-center gx-4">
          <div class="col-md-5">
            <div class="ms-md-2 ms-lg-5" data-aos="fade-down">
              <img class="img-fluid rounded-3" src="../public/img/makanan1.png" />
            </div>
          </div>
          <div class="col-md-6 offset-md-1">
            <div class="ms-md-2 ms-lg-5" data-aos="fade-up">
              <span class="text-muted">Baca Juga</span>
              <h2 class="display-5 fw-bold">Tentang Kami</h2>
              <p class="lead" style="text-align: justify">
                Healthy Food hadir untuk memberikan rekomendasi menu makanan dari posyandu yang
                efektif mencegah stunting. Setiap menu dilengkapi bahan-bahan dan cara memasaknya
                agar mudah dipraktikkan.
              </p>
              <p class="lead mb-0" style="text-align: justify">
                Kami juga memastikan resep diawasi oleh ahli gizi, sehingga memenuhi kebutuhan
                nutrisi harian anak dan keluarga untuk mendukung tumbuh kembang optimal.
              </p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!--Section Menu Makanan-->
    <section class="py-5" id="menumakanan">
      <div class="container">
        <div class="row justify-content-center text-center mb-4 mb-md-5">
          <div class="col-xl-9 col-xxl-8">
            <span class="text-muted">Rekomendasi</span>
            <h2 class="display-5 fw-bold">Menu Makanan Sehat</h2>
            <p class="lead">
              Berikut ini kami rekomendasikan makanan sehat yang efektif dalam mencegah stunting
              ilengkapi dengan panduan bahan-bahan dan cara memasaknya.
            </p>
          </div>
        </div>
        <div class="row g-5">
          <div
            class="col-md-4"
            v-for="(recipe, index) in recipes.slice(0, displayedRecipes)"
            :key="recipe.recipe_name"
            @click="openModal(recipe)"
          >
            <a href="javascript:void(0)" class="text-decoration-none">
              <div class="card border-0 bg-light-subtle shadow-lg rounded">
                <img
                  :src="recipe.image"
                  :alt="recipe.recipe_name"
                  class="img-fluid rounded-top-1"
                  style="width: 100%; height: 300px"
                />
                <div class="card-body p-0 text-center mt-4">
                  <h5 class="text-dark text-decoration-none fw-bolder">
                    {{ recipe.recipe_name }}
                  </h5>
                  <p class="mt-3" style="color: #349d63">Lihat resep makanan selengkapnya -></p>
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
        <div class="modal-dialog modal-dialog-centered">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title fw-bolder fs-4">{{ selectedRecipe.recipe_name }}</h5>
              <button
                type="button"
                class="btn-close"
                aria-label="Close"
                @click="closeModal"
              ></button>
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
  </main>
</template>
