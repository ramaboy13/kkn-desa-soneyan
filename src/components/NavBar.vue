<template>
  <nav class="navbar navbar-blur fixed-top navbar-expand-lg">
    <div class="container">
      <a href="#" class="navbar-brand" :class="absoluteClass">
        <img src="/img/logo.png" alt="logo" width="50" height="50" />
        <span class="d-none d-sm-inline ps-2 px-auto fs-6">KKN UMK DESA SENOYAN</span>
      </a>

      <button
        class="navbar-toggler ms-auto"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarNav"
        aria-controls="navbarNav"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav mx-auto">
          <li class="nav-item">
            <a to="/" class="nav-link" aria-current="page"> Home </a>
          </li>
          <li class="nav-item">
            <a to="/about" class="nav-link"> About </a>
          </li>
          <li class="nav-item">
            <a to="/contact" class="nav-link"> Contact </a>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      isMobileView: false
    }
  },
  computed: {
    absoluteClass() {
      return this.isMobileView ? '' : 'position-absolute'
    }
  },
  mounted() {
    this.checkWindowSize()
    window.addEventListener('resize', this.checkWindowSize)
  },
  beforeUnmount() {
    window.removeEventListener('resize', this.checkWindowSize)
  },
  methods: {
    checkWindowSize() {
      this.isMobileView = window.innerWidth < 992
    }
  }
}
</script>
