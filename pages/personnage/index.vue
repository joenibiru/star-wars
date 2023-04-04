<template>
  <div class="personnage">
     <h1>Personnages</h1>
    <div class="container px-4 text-center">
    <div class="row gx-5">
      <div class="col-md-4" v-for="(perso, index) in personnages" :key="index">
        <div class="p-3">
          <div class="card bg-dark" style="width: 18rem; border-color: #fbb040;">
            <img :src="perso.personnageImage" class="card-img-top" />
            <div class="card-body">
              <h5 class="card-title text-warning">{{ perso.name }}</h5>
              <NuxtLink :to="{
                name: 'personnage-slug',
                params: { slug: perso.name.toLowerCase().replace(/ /g, '-') }
              }" class="btn btn-warning">
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
      personnages: [],
    };
  },
  async created() {
    // Appel initial à l'API pour récupérer le premier lot de personnages
    const result = await fetch('https://swapi.dev/api/people/').then((res) => res.json());
    this.personnages = result.results.map((personnage) => ({
      ...personnage,
      personnageImage: `https://starwars-visualguide.com/assets/img/characters/${parseInt(personnage.url.replace(/\D/g, ''))}.jpg`
    }));

    // Récupération des autres lots de personnages en utilisant la pagination de l'API
    let nextPage = result.next;
    while (nextPage) {
      const nextResult = await fetch(nextPage).then((res) => res.json());
      this.personnages = [...this.personnages, ...nextResult.results.map((personnage) => ({
        ...personnage,
        personnageImage: `https://starwars-visualguide.com/assets/img/characters/${parseInt(personnage.url.replace(/\D/g, ''))}.jpg`
      }))];
      nextPage = nextResult.next;
    }
  },

};
</script>
<style scoped>
.personnage{
  background-image: url(~assets/images/a9ac4e5ef98fb5e554a9faa4f548749e.jpg);
}

h1{
  color: rgb(195, 255, 0);
  font-family: 'Star Wars', sans-serif;
  text-align: center;
  padding: 30px;
}

.card {
  border: none;
  box-shadow: 0 0 20px #ffd700;
}

.card-title,
.card-text {
  color: rgb(195, 255, 0);
  font-family: 'Star Wars', sans-serif;
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