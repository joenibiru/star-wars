<template>
  <div class="slug pb-0">
    <div class="container">
      <div class="row mt-4">
        <div class="col-md-6">
          <img :src="planete?.image" :alt="planete?.name" class="img-fluid rounded">
        </div>
        <div class="col-md-6 d-flex flex-column justify-content-center align-items-center bg-dark p-5">
          <h2 class="text-warning mb-4" v-if="planete && planete.name">
            {{ planete.name }}
          </h2>
          <div class="mt-4" v-if="planete">
            <ul class="list-unstyled">
              <li><strong>Période de rotation:</strong> {{ planete.rotation_period }} heures</li>
              <li><strong>Période orbitale:</strong> {{ planete.orbital_period }} jours</li>
              <li><strong>Diamètre:</strong> {{ planete.diameter }} km</li>
              <li><strong>Climat:</strong> {{ planete.climate }}</li>
              <li><strong>Gravité:</strong> {{ planete.gravity }}</li>
              <li><strong>Terrain:</strong> {{ planete.terrain }}</li>
              <li><strong>Surface d'eau:</strong> {{ planete.surface_water }} km</li>
              <li><strong>Population:</strong> {{ planete.population }} habitants</li>
            </ul>
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
    const response = await fetch(`https://swapi.dev/api/planets/?search=${slug}`);
    const { results } = await response.json();
    const [planete] = results;
    const imageId = parseInt(planete.url.match(/(\d+)\/$/)[1]);
    const image = `https://starwars-visualguide.com/assets/img/planets/${imageId}.jpg`;
    planete.image = image;

    if (planete.residents && planete.residents.length) {
      const residentPromises = planete.residents.map(url => fetch(url).then(response => response.json()));
      const residents = await Promise.all(residentPromises);
      const habitants = residents.map(resident => resident.name);
      return { planete, habitants };
    } else {
      return { planete };
    }
  },
};
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

ul li {
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

</style>
