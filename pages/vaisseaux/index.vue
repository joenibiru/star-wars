<template>
  <div class="main vaisseaux">
    <div class="container">
      <div class="row">
        <div class="titre text-center ">
          <h1>Vaisseaux</h1>
        </div>
      </div>
      <div class="row card_content">
        <div v-for="(vaisseau, index) in vaisseaux" :key="index" class="col-md-4">
          <div :class="['card', 'mb-4', 'shadow-sm', {'d-none': !vaisseau.imageLoaded}]">
            <img :src="vaisseau.image" :alt="vaisseau.nom" class="card-img-top" style="height: 200px; object-fit: cover;" @load="vaisseau.imageLoaded = true" @error="vaisseau.imageLoaded = false">
            <div class="card-body">
              <h5 class="card-title">{{ vaisseau.nom }}</h5>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
  
<script>
export default {
  data() {
    return {
      vaisseaux: []
    }
  },
  mounted() {
    fetch("https://swapi.dev/api/starships/")
      .then(response => response.json())
      .then(data => {
        this.vaisseaux = data.results.map(vaisseau => ({
          nom: vaisseau.name,
          image: `https://starwars-visualguide.com/assets/img/starships/${this.getIdFromUrl(vaisseau.url)}.jpg`,
          imageLoaded: false
        }));
      })
  },
  methods: {
    getIdFromUrl(url) {
      return url.match(/(\d+)\/$/)[1];
    }
  }
}
</script>
  
<style scoped>
.titre {
  color: rgb(195, 255, 0);
  font-family: 'Star Wars', sans-serif;
}

.vaisseaux {
  width: 100%;
  background-image: url(~assets/images/a9ac4e5ef98fb5e554a9faa4f548749e.jpg);
  background-repeat: repeat;
  background-color: transparent;
  background-position: center;
}

.card_content {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}
</style>
