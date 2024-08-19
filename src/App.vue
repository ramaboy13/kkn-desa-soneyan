<script setup>
import NavBar from './components/NavBar.vue'
import FoodSection from './components/FoodSection.vue'
import FooterApp from './components/FooterApp.vue'
</script>

<template>
  <main>
    <!-- NavBar -->
    <NavBar></NavBar>

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
                ><i class="bi bi-play-fill"></i
              ></a>
            </div>
          </div>
        </div>
        <a
          class="position-absolute bottom-0 start-50 translate-middle text-primary"
          href="#scrollToContent"
          ><i class="bi bi-arrow-down"></i
        ></a>
      </div>
    </section>

    <!--Section Menu Makanan-->
    <FoodSection></FoodSection>

    <!-- Footer -->
    <FooterApp></FooterApp>
  </main>
</template>

<style scoped>
* {
  font-family: 'inter', sans-serif;
  scroll-behavior: smooth;
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
  background-color: rgba(176, 176, 176, 0.53);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background-color: rgb(240, 240, 240);
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
