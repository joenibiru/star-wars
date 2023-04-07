<template>
  <div class="vehicules">
    <h1>Vehicules</h1>
    <div class="container px-4 text-center">
      <div class="row gx-5">
        <div class="col-md-4" v-for="(vehicule, index) in vehicules" :key="index">
          <div class="p-3">
            <div class="card bg-dark" style="width: 18rem;">
              <img :src="vehicule.vehiculeImage" class="card-img-top" />
              <div class="card-body">
                <h5 class="card-title text-warning">{{ vehicule.name }}</h5>
                <NuxtLink v-if="vehicule && vehicule.name !== undefined" :to="{
                  name: 'vehicules-slug',
                  params: { slug: vehicule.name.toLowerCase().replace(/ /g, '-') }
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
      vehicules: [],
    };
  },
  async created() {
    // Appel initial à l'API pour récupérer le premier lot de véhicules
    const result = await fetch('https://swapi.dev/api/vehicles/').then((res) => res.json());
    this.vehicules = result.results.map((vehicule) => ({
      ...vehicule,
      vehiculeImage: `https://starwars-visualguide.com/assets/img/vehicles/${parseInt(
        vehicule.url.replace(/\D/g, '')
      )}.jpg`,
    }));

    // Récupération des autres lots de véhicules en utilisant la pagination de l'API
    let nextPage = result.next;
    while (nextPage) {
      const nextResult = await fetch(nextPage).then((res) => res.json());
      this.vehicules = [
        ...this.vehicules,
        ...nextResult.results.map((vehicule) => ({
          ...vehicule,
          vehiculeImage: `https://starwars-visualguide.com/assets/img/vehicles/${parseInt(
            vehicule.url.replace(/\D/g, '')
          )}.jpg`,
        })),
      ];
      nextPage = nextResult.next;
    }
  },
};
</script>

<style scoped>
.vehicules {
  background-image: url(~assets/images/a9ac4e5ef98fb5e554a9faa4f548749e.jpg);
}

h1 {
  color: rgb(195, 255, 0);
  font-family: 'Star Wars', sans-serif;
  padding: 30px;
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