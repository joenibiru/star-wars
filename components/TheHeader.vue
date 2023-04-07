<template>
  <header class="bg-dark">
    <div class="container">
      <div class="row align-items-center justify-content-center">
        <div class="col-12 col-md-2 order-md-3">
          <Logo />
        </div>
        <div class="category col-12 col-md-6 d-flex justify-content-center justify-content-md-start order-md-2">
          <NuxtLink to="/personnage" class="nav-link ">Personnages</NuxtLink>
          <NuxtLink to="/planetes" class="nav-link ">Planetes</NuxtLink>
          <NuxtLink to="/vaisseaux" class="nav-link ">Vaisseaux</NuxtLink>
          <NuxtLink to="/vehicules" class="nav-link ">Vehicules</NuxtLink>
          <NuxtLink to="/especes" class="nav-link ">Especes</NuxtLink>
        </div>
        <div class="col-12 col-md-3 d-flex sabre-container position-relative">
          <div class="sabre position-absolute top-0 start-50 translate-middle" style="transform: rotate(45deg);">
            <img src="~assets/images/star-wars-sabe.png" alt="sabre laser" width="200px" @mouseover="playSound">
          </div>
          <div class="sabre_laser position-absolute top-0 start-50 translate-middle" style="transform: rotate(-45deg);">
            <img src="~assets/images/star-wars-sabre laser.png" alt="sabre laser" width="200px" @mouseover="playSound">
          </div>
        </div>
      </div>
    </div>
  </header>
</template>

<script>
import Logo from './logo.vue';

export default {
  name: "index.vue",
  components: { Logo },
  methods: {
    playSound() {
      const audio = new Audio('/song/Sabrelaser[bruitage]_34.mp3');
      audio.play();
    }
  }
}
</script>

<style scoped>
header {
  background-image: url(~assets/images/a9ac4e5ef98fb5e554a9faa4f548749e.jpg);
  position: relative;
}

.sabre-container {
  height: 100px;
}

.sabre,
.sabre_laser {
  z-index: 1;
}

@media (min-width: 768px) {
  .nav-link {
    font-size: 14px;
    color: rgb(195, 255, 0);
    font-family: 'Star Wars', sans-serif;
  }
}
.category{

  margin-right: 100px;
}
</style>

