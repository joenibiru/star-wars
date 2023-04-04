<template>
  <div class="main">
    <div class="container">
      <div class="row justify-content-center text-center">
        <div class="col-md-4">
          <div class="card">
            <div class="card-body">
              <NuxtLink to="/personnage">
                <img src="~assets/images/dark vador.jpg" alt="" width="300px" height="300px">
              </NuxtLink>
            </div>
          </div>
        </div>

        <div class="col-md-4">
          <div class="card">
            <div class="card-body">
              <NuxtLink to="/planetes">
                <img src="~assets/images/Yavin4.webp" alt="" width="300px" height="300px">
              </NuxtLink>
            </div>
          </div>
        </div>
        <div class="col-md-4">
          <div class="card">
            <div class="card-body">
              <NuxtLink to="/vaisseaux">
                <img src="~assets/images/MillFal_thumb.jpg" alt="" width="300px" height="300px">
              </NuxtLink>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'IndexPage'
}
</script>

<style scoped>
.main {
  background-image: url(~assets/images/a9ac4e5ef98fb5e554a9faa4f548749e.jpg);
  padding-right: 0;
  padding-left: 0;
}

.card {
  background-color: transparent;
}

img {
  margin-top: 20px;
  margin-bottom: 20px;
  border-radius: 150px;
  box-shadow: 0 0 10px #ffd700;
  border: solid #ffd700 3px;
}
</style>
