<template>
    <div class="container px-4 text-center">
      <div class="row gx-5">
        <div class="col-md-4">
          <div class="p-3">
            <div class="card bg-dark" style="width: 18rem; border-color: #fbb040;">
              <img src="" class="card-img-top">
              <div class="card-body">
                <h5 class="card-title text-warning">{{ name }}</h5>
                <p class="card-text text-white">Le vaisseau le plus rapide de la galaxie, capable de parcourir des distances
                  interstellaires en un rien de temps.</p>
                <a href="/personnage/slug" class="btn btn-warning">Explorer</a>
              </div>
            </div>
          </div>
        </div>
    </div>
  </div>
  </template>
  
  <script>
  
  export default {
    props: {
      name: {
        type: String,
        required: true
        }
    }
  }
  </script>