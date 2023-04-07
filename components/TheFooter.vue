<template>
  <footer class="text-center">
    <div class="container">
      <div class="row justify-content-center">
        <div class="col-md-4">
          <NuxtLink to="/MentionsLegale" class="text-decoration-none">Mentions legales</NuxtLink>
        </div>

        <div class="col-md-4">
          <NuxtLink to="/Contact" class="text-decoration-none">Contact</NuxtLink>
        </div>

        <div class="col-md-4">
          <NuxtLink to="/Developpement" class="text-decoration-none">Developpement</NuxtLink>
        </div>
      </div>
    </div>
  </footer>
</template>
  
<script>

export default {
  name: 'index.vue'
}
</script>
  
<style scoped>
footer {
  background-image: url(~assets/images/a9ac4e5ef98fb5e554a9faa4f548749e.jpg);
  padding-top: 30px;
  padding-bottom: 30px;
  height: auto;
}

footer a {
  font-family: 'Star Wars', sans-serif;
}

footer a:hover {
  color: #ffd700;
}
</style>
  