<template>
    <div class="card-p">
      <div class="card--img">
        <img :src="image" :alt="name">
      </div>
      <div class="card--text">
        <h1>{{ name }}</h1>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      name: {
        type: String,
        required: true
      },
      image: {
        type: String,
        required: true
      }
    }
  }
  </script>
  
  <style scoped>
  .card-p {
    background-color: white;
    display: flex;
    flex-wrap: wrap;
    border: solid #220353 3px;
    box-shadow: 0 0 20px #ffd700;
    width: 300px;
    height: 400px;
    padding: 15px;
    margin-right: 20px;
    margin-bottom: 20px;
  }
  
  .card--img {
    flex-grow: 1;
    display: flex;
    justify-content: center;
  }
  
  .card--img img {
    max-width: 80%;
    max-height: 80%;
    object-fit: contain;
  }
  
  .card--text {
    flex-grow: 1;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
  }
  
  .card--text h1 {
    font-size: 24px;
    color: #ffd700;
    font-weight: bold;
    text-transform: uppercase;
    margin: 0;
  }
  </style>
  