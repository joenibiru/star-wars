<template>
  <div class="main_vaisseaux">
    <div class="container">
      <div class="row">
        <div class="titre text-center">
          <h1>Vaisseaux</h1>
        </div>
      </div>
      <div class="row card_content">
        <div v-for="(vaisseau, index) in vaisseaux" :key="index" class="col-md-4">
          <NuxtLink :to="'/vaisseaux/' + vaisseau.slug">
            <div class="card-v bg-dark">
              <div class="card--img">
                <img :src="vaisseau.image" :alt="vaisseau.nom" @load="vaisseau.imageLoaded = true" @error="vaisseau.imageLoaded = false">
              </div>
              <div class="card--text">
                <h1>{{ vaisseau.nom }}</h1>
              </div>
            </div>
          </NuxtLink>
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
    this.getStarships('https://swapi.dev/api/starships/');
  },
  methods: {
    getStarships(url) {
      fetch(url)
        .then(response => response.json())
        .then(data => {
          this.vaisseaux = this.vaisseaux.concat(data.results.map(vaisseau => ({
            nom: vaisseau.name,
            image: `https://starwars-visualguide.com/assets/img/starships/${this.getIdFromUrl(vaisseau.url)}.jpg`,
            imageLoaded: false
          })));
          if (data.next) {
            this.getStarships(data.next);
          }
        });
    },
    getIdFromUrl(url) {
      return url.match(/(\d+)\/$/)[1];
    }
  }
}
</script>

<style scoped>
.main_vaisseaux{
background-image: url("~assets/images/a9ac4e5ef98fb5e554a9faa4f548749e.jpg");
}
.titre{
  color: rgb(204, 255, 0);
  font-family: "Star Wars", sans-serif;
}
.card-v {
  background-color: white;
  display: flex;
  flex-direction: column;
  border: solid #220353 3px;
  box-shadow: 0 0 20px #ffd700;
  width: 300px;
  height: 300px;
  padding: 15px;
  margin-right: 20px;
  margin-bottom: 20px;
  overflow: hidden;
  border-radius: 10px;
}

.card--img {
  flex-grow: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
}

.card--img img {
  max-width: 100%;
  max-height: 100%;
  object-fit: cover;
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  margin: auto;
}

.card--text {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  padding: 1rem;
  background-color: rgba(34, 3, 83, 0.8);
  border-top: solid #ffd700 2px;
}

.card--text h1 {
  font-size: 24px;
  color: #ffd700;
  font-weight: bold;
  text-transform: uppercase;
  margin: 0;
}
</style>

