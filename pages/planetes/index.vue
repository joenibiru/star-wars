<template>
    <div class="main planetes">
      <div class="container">
        <div class="row">
          <div class="titre text-center">
            <h1>Planetes</h1>
          </div>
        </div>
        <div class="row card_content">
          <Planetes v-for="(planete, index) in planetes" :key="index" :name="planete.name" :image="planete.image" />
        </div>
      </div>
    </div>
  </template>
  <script>
  import Planete from '~/components/Planetes.vue';
  
  export default {
    components: {
      Planete,
    },
    data() {
      return {
        planetes: [],
      };
    },
    async created() {
      // Appel initial à l'API pour récupérer le premier lot de planètes
      const result = await fetch('https://swapi.dev/api/planets/').then((res) => res.json());
      this.planetes = result.results;
  
      // Récupération des autres lots de planètes en utilisant la pagination de l'API
      let nextPage = result.next;
      while (nextPage) {
        const nextResult = await fetch(nextPage).then((res) => res.json());
        this.planetes = [...this.planetes, ...nextResult.results];
        nextPage = nextResult.next;
      }
  
      // Récupération des images des planètes
      this.planetes.forEach(async (planete) => {
        const imageId = parseInt(planete.url.match(/(\d+)\/$/)[1]);
        const image = `https://starwars-visualguide.com/assets/img/planets/${imageId}.jpg`;
        planete.image = image;
      });
    },
  };
  </script>
  <style scoped>
  .titre {
    color: rgb(204, 255, 0);
    font-family: "Star Wars", sans-serif;
  }
  
  .planetes {
    width: 100%;
    background-image: url("~assets/images/a9ac4e5ef98fb5e554a9faa4f548749e.jpg");
  }
  
  .card_content {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
  }
  </style>