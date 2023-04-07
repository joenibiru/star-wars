<template>
  <div class="error-page">
    <span class="error-code">404</span>
  </div>
</template>

<style scoped>
  .lightning {
    width: 100%;
    max-width: 400px;
  }
  
  .error-code {
    font-size: 10rem;
    font-weight: bold;
    text-shadow: 2px 2px #ffea00;
    color: rgb(204, 255, 0);
  font-family: "Star Wars", sans-serif;
  }

  .error-page {
    background: url('~assets/images/Palpatine-Force-Lightning.jpg');
    background-size: cover;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    font-size: 3rem;
    color: white;
  }
</style>
