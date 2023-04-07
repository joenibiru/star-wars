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
          <p class="mb-4" v-if="personnage && personnage.speciesList">
            Espèces : {{ personnage.speciesList }}
          </p>
          <p class="mb-4" v-if="personnage && personnage.height">
            Taille : {{ personnage.height }} cm
          </p>
          <p class="mb-4" v-if="personnage && personnage.mass">
            Poids : {{ personnage.mass }} kg
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
          <p class="mb-4" v-if="personnage && personnage.starshipList">
            Vaisseaux : {{ personnage.starshipList }}
          </p>
          <p class="mb-4" v-if="personnage && personnage.vehiclesList">
            Véhicules : {{ personnage.vehiclesList }}
          </p>
          <p class="mb-4" v-if="personnage && personnage.homeworld">
            Planète : {{ nomPlanete }}
          </p>
        </div>
        <div class="col-md-12">
          <div class="row">
            <h4 class="text-warning mb-4 mx-auto" v-if="films.length">
              Films
            </h4>
          </div>
          <div class="row">
            <div class="col-md-4 mb-4" v-for="film in films" :key="film.episode_id">
              <div class="card  text-white">
                <img :src="film.image" :alt="film.title" class="card-img-top">
                <div class="card-body">
                  <h5 class="card-title">{{ film.title }}</h5>
                </div>
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
  async asyncData({ params }) {
    const slug = params.slug.replace(/-/g, ' ');
    const response = await fetch(`https://swapi.dev/api/people/?search=${slug}`);
    const { results } = await response.json();
    const [personnage] = results;
    const imageId = parseInt(personnage.url.match(/(\d+)\/$/)[1]);
    const image = `https://starwars-visualguide.com/assets/img/characters/${imageId}.jpg`;
    personnage.image = image;

    if (personnage.vehicles) {
      const vehiclePromises = personnage.vehicles.map(url => fetch(url).then(response => response.json()));
      const vehicleResults = await Promise.all(vehiclePromises);

      // Add image URLs to vehicle objects
      const vehicleImagePromises = vehicleResults.map(async vehicle => {
        const id = parseInt(vehicle.url.match(/(\d+)\/$/)[1]);
        const imageUrl = `https://starwars-visualguide.com/assets/img/vehicles/${id}.jpg`;
        try {
          const response = await fetch(imageUrl);
          return response.ok ? imageUrl : null;
        } catch (error) {
          return null;
        }
      });

      const vehicleImageResults = await Promise.all(vehicleImagePromises);

      const vehicles = vehicleResults.map((vehicle, index) => {
        vehicle.image = vehicleImageResults[index];
        return vehicle;
      });

      personnage.vehicles = vehicles;

      // Create comma-separated string of vehicle names
      const vehicleNames = vehicles.map(vehicle => vehicle.name);
      const vehiclesList = vehicleNames.join(", ");
      personnage.vehiclesList = vehiclesList;
    }

    return { personnage };
  },

  async created() {
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

    if (this.personnage && this.personnage.films) {
      const filmPromises = this.personnage.films.map(url => fetch(url).then(response => response.json()));
      const filmResults = await Promise.all(filmPromises);

      if (this.personnage && this.personnage.starships) {
        const starshipPromises = this.personnage.starships.map(url => fetch(url).then(response => response.json()));
        const starshipResults = await Promise.all(starshipPromises);
        const starshipNames = starshipResults.map(starship => starship.name);
        const starshipList = starshipNames.join(", ");
        this.personnage.starshipList = starshipList;
      }

      if (this.personnage && this.personnage.species) {
        const speciesPromises = this.personnage.species.map(url => fetch(url).then(response => response.json()));
        const speciesResults = await Promise.all(speciesPromises);
        const speciesNames = speciesResults.map(species => species.name);
        const speciesList = speciesNames.join(", ");
        this.personnage.speciesList = speciesList;
      }

      // Add image URLs to film objects
      const filmImagePromises = filmResults.map(film => {
  const id = parseInt(film.url.match(/(\d+)\/$/)[1]);
  const imageUrl = `https://starwars-visualguide.com/assets/img/films/${id}.jpg`;
  return fetch(imageUrl)
    .then(response => response.blob())
    .then(blob => {
      return URL.createObjectURL(blob);
    })
    .catch(error => null);
});

const filmImageResults = await Promise.all(filmImagePromises);

this.films = filmResults.map((film, index) => {
  film.image = filmImageResults[index];
  return film;
});

    }
  },

  data() {
    return {
      nomPlanete: '',
      films: []
    }
  }
}
</script>


<style scoped>
.slug {
  background-image: url('~assets/images/a9ac4e5ef98fb5e554a9faa4f548749e.jpg');
  padding-top: 60px;
  padding-bottom: 0;
}


.img-fluid {
  max-width: 100%;
  height: auto;
  padding: 30px;

}

.col-md-6.d-flex.flex-column.justify-content-center.align-items-center.bg-dark.p-5 {
  border-radius: 10px;
}

h4 {
  padding: 40px;
  font-size: 30px;
  font-family: 'Star Wars', sans-serif;
}

p,
h5 {
  color: #FFE81F;
  font-size: 20px;
  margin-bottom: 1.5rem;
}

h2 {
  color: #FFE81F;
  font-size: 30px;
  font-weight: bold;
  margin-bottom: 1.5rem;
}

li {
  color: #FFE81F;
  font-size: 20px;
  margin-bottom: 1.5rem;
}

.card {
  background-color: transparent;
  border: none;
}

.card-header {
  background-color: #FFE81F;
  color: #262626;
  font-weight: bold;
}

.card-body {
  padding: 0;
}

.card-text {
  color: #FFE81F;
  font-size: 20px;
  margin-bottom: 1.5rem;
}

.card-img-top {
  max-width: 100%;
  height: auto;
  padding: 30px;
}

.card-title {
  text-align: center;
}
</style>
