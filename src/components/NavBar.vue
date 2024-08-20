<template>
  <nav class="navbar navbar-blur fixed-top navbar-expand-lg">
    <div class="container">
      <a href="#" class="navbar-brand" :class="absoluteClass">
        <img src="/img/logo.png" alt="logo" width="50" height="50" />
        <span class="d-none d-sm-inline ps-2 px-auto fs-6 fw-bolder display-5"
          >KKN UMK DESA SONEYAN</span
        >
      </a>

      <button
        class="navbar-toggler ms-auto my-auto"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarNav"
        aria-controls="navbarNav"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse justify-content-end" id="navbarNav">
        <ul class="navbar-nav">
          <li class="nav-item">
            <a href="#beranda" class="nav-link" aria-current="page">Beranda</a>
          </li>
          <li class="nav-item">
            <a href="#tentangkami" class="nav-link">Tentang Kami</a>
          </li>
          <li class="nav-item">
            <a href="#makanansehat" class="nav-link">Menu Makanan</a>
          </li>
          <li class="nav-item">
            <a href="#kontakkami" class="nav-link">Kontak Kami</a>
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

    document.querySelectorAll('.navbar-nav .nav-item').forEach(function (li) {
      li.addEventListener('click', function () {
        // Temukan elemen a di dalam li dan klik
        const link = li.querySelector('a')
        if (link) {
          link.click()
        }
      })
    })
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
