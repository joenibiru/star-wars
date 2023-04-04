<template>
  <header>
    <div class="container">
      <div class="row align-items-center">
        <div class="col-2">
          <Logo />
        </div>
        <div class="col-2">
          <NuxtLink to="/personnage" class="text-decoration-none">Personnages</NuxtLink>
        </div>
        <div class="col-2">
          <NuxtLink to="/planetes" class="text-decoration-none">Planetes</NuxtLink>
        </div>
        <div class="col-2">
          <NuxtLink to="/vaisseaux" class="text-decoration-none">Vaisseaux</NuxtLink>
        </div>
        <div class="sabre">
          <img src="~assets/images/star-wars-sabe.png" alt="sabre laser" width="500px" @mouseover="playSound"  >
        </div>
        <div class="sabre_laser">
          <img src="~assets/images/star-wars-sabre laser.png" alt="sabre laser" width="500px" @mouseover="playSound"  >
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
}
.sabre_laser{
  margin-left: 140px;
  
}


header a {
  font-family: 'Star Wars', sans-serif;
}

header a:hover {
  color: #ffd700;
}
</style>
