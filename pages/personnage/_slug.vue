<template>
  <div class="slug pb-0">
    <div class="container">
      <div class="row mt-4">
        <div class="col-md-6">
          <img :src="personnage?.image" :alt="personnage?.name" class="img-fluid rounded">
        </div>
        <div class="col-md-6 d-flex flex-column justify-content-center align-items-center bg-dark p-5">
          <h2 class="text-warning mb-4" v-if="personnage && personnage.name">
            {{ personnage.name }}
          </h2>
          <h5 class="mb-4" v-if="personnage && personnage.gender">
            Genre : {{ personnage.gender }}
          </h5>
          <p class="mb-4" v-if="personnage && personnage.mass">
            Poids : {{ personnage.mass }}
          </p>
          <p class="mb-4" v-if="personnage && personnage.eye_color">
            Couleur des yeux : {{ personnage.eye_color }}
          </p>
          <p class="mb-4" v-if="personnage && personnage.hair_color">
            Couleur de cheveux : {{ personnage.hair_color }}
          </p>
          <p class="mb-4" v-if="personnage && personnage.skin_color">
            Couleur de peau : {{ personnage.skin_color }}
          </p>
          <p class="mb-4" v-if="personnage && personnage.birth_year">
            Date de naissance : {{ personnage.birth_year }}
          </p>
          <p class="mb-4" v-if="personnage && personnage.homeworld">
            Planètes : {{ nomPlanete }}
          </p>

          <button class="btn btn-warning btn-lg text-uppercase font-weight-bold shadow mb-4">
            Rejoignez le côté obscur
          </button>
          <button class="btn btn-outline-warning btn-lg text-uppercase font-weight-bold">
            FILM
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ params }) {
    const slug = params.slug.replace(/-/g, ' ');
    const response = await fetch(`https://swapi.dev/api/people/?search=${slug}`);
    const { results } = await response.json();
    const [personnage] = results;
    const imageId = parseInt(personnage.url.match(/(\d+)\/$/)[1]);
    const image = `https://starwars-visualguide.com/assets/img/characters/${imageId}.jpg`;
    personnage.image = image;
    return { personnage };
  },
  created() {
    if (this.personnage && this.personnage.homeworld) {
      fetch(this.personnage.homeworld)
        .then(response => response.json())
        .then(data => {
          const nomPlanete = data.name;
          console.log(`Le personnage est originaire de la planète ${nomPlanete}.`);
          this.nomPlanete = nomPlanete;
        })
        .catch(error => {
          console.error('Erreur lors de la récupération des informations sur la planète.', error);
        });
    }
  },
  data() {
    return {
      nomPlanete: '',
      films: []
    }
  },
}
</script>



<style scoped>
.slug {
  background-image: url('~assets/images/a9ac4e5ef98fb5e554a9faa4f548749e.jpg');
  padding-top: 60px;
  padding-bottom: 0;
}

.btn-warning {
  background-color: #FFE81F;
  color: #001635;
  border-color: #FFE81F;
}

.btn-warning:hover {
  background-color: #001635;
  color: #FFE81F;
  border-color: #FFE81F;
}

.img-fluid {
  max-width: 100%;
  height: auto;
  padding: 30px;
}

p {
  color: #FFE81F;
  font-size: 20px;
}

h5 {
  color: #FFE81F;
  font-size: 20px;
}
</style>
