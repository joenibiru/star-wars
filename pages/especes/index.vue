<template>
    <div class="especes">
      <h1 class="text-center py-5">Especes</h1>
      <div class="container">
        <div class="row row-cols-1 row-cols-md-3 g-4">
          <div class="col" v-for="(espece, index) in especes" :key="index">
            <div class="card h-100 bg-dark">
              <img :src="espece.image" class="card-img-top" alt="">
              <div class="card-body d-flex flex-column justify-content-between">
                <h5 class="card-title text-warning">{{ espece.name }}</h5>
                <div class="mt-3">
                  <NuxtLink v-if="espece && espece.name !== undefined" :to="{
                    name: 'especes-slug',
                    params: { slug: espece.name.toLowerCase().replace(/ /g, '-') }
                  }" class="btn btn-warning w-100">
                    Explorer
                  </NuxtLink>
                </div>
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
        especes: [],
      };
    },
    async created() {
      // Appel initial à l'API pour récupérer le premier lot d'espèces
      const result = await fetch('https://swapi.dev/api/species/').then((res) => res.json());
      this.especes = result.results.map((espece) => ({
        ...espece,
        image: `https://starwars-visualguide.com/assets/img/species/${parseInt(
          espece.url.replace(/\D/g, '')
        )}.jpg`,
      }));
  
      // Récupération des autres lots d'espèces en utilisant la pagination de l'API
      let nextPage = result.next;
      while (nextPage) {
        const nextResult = await fetch(nextPage).then((res) => res.json());
        this.especes = [
          ...this.especes,
          ...nextResult.results.map((espece) => ({
            ...espece,
            image: `https://starwars-visualguide.com/assets/img/species/${parseInt(
              espece.url.replace(/\D/g, '')
            )}.jpg`,
          })),
        ];
        nextPage = nextResult.next;
      }
    },
  };
  </script>
  
  <style scoped>
  .especes {
    background-image: url(~assets/images/a9ac4e5ef98fb5e554a9faa4f548749e.jpg);
    padding-bottom: 80px;
  }
  
  h1 {
    color: rgb(195, 255, 0);
    font-family: 'Star Wars', sans-serif;
    font-size: 42px;
  }
  
  .card {
    border: solid #220353 3px;
    box-shadow: 0 0 20px #ffd700;
    border-radius: 10px;
  }
  
  .card-title,
  .card-text {
    color: rgb(195, 255, 0);
    font-weight: bold;
  }
  
  .card-body {
    font-weight: bold;
    border-top: 3px solid #fbb040;
  }
  
  .btn-warning {
    color: #141414;
    font-family: 'Star Wars', sans-serif;
  }
  
  .btn-warning:hover {
    background-color: #fbb040;
    border-color: #fbb040;
    color: #141414;
  }
  </style>