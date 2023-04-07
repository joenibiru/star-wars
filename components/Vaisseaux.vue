<template>
    <div class="card-v">
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
.card-v {
  background-color: white;
  display: flex;
  flex-direction: column;
  border: solid #220353 3px;
  box-shadow: 0 0 20px #ffd700;
  width: 300px;
  height: 400px;
  padding: 15px;
  margin-right: 20px;
  margin-bottom: 20px;
  overflow: hidden;
  border-radius: 10px;
}

.card--img {
  flex-grow: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
}

.card--img img {
  max-width: 100%;
  max-height: 100%;
  object-fit: cover;
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  margin: auto;
}

.card--text {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  padding: 1rem;
  background-color: rgba(34, 3, 83, 0.8);
}

.card--text h1 {
  font-size: 24px;
  color: #ffd700;
  font-weight: bold;
  text-transform: uppercase;
  margin: 0;
}
</style>
