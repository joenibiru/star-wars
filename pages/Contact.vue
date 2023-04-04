<template>
  <div class="main contact">
    <div class="contact-page container py-5">
      <div class="row">
        <div class="col-lg-8 mx-auto">
          <h1 class="text-center mb-4">Contactez-nous</h1>
          <p>Pour toute question ou demande, n'hesitez pas a nous contacter en remplissant le formulaire ci-dessous :</p>

          <form @submit.prevent="submitForm">
            <div class="form-group">
              <label for="name">Nom :</label>
              <input type="text" id="name" v-model="name" class="form-control" required>
            </div>

            <div class="form-group">
              <label for="email">E-mail :</label>
              <input type="email" id="email" v-model="email" class="form-control" required>
            </div>

            <div class="form-group">
              <label for="message">Message :</label>
              <textarea id="message" v-model="message" class="form-control" required></textarea>
            </div>

            <button type="submit" class="btn btn-primary">Envoyer</button>
          </form>

          <div v-if="sent" class="success-message mt-3">
            <p class="alert alert-success">Votre message a ete envoye avec succes !</p>
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
      name: '',
      email: '',
      message: '',
      sent: false
    }
  },

  methods: {
    submitForm() {
      // Code pour envoyer le formulaire ici
      // Ici, nous allons simplement afficher un message de succès
      this.sent = true;
    }
  }
}
</script>

<style scoped>
.main.contact {
  background-image: url(~assets/images/a9ac4e5ef98fb5e554a9faa4f548749e.jpg);
}

h1 {
  color: rgb(212, 255, 0);
  font-family: 'Star Wars', sans-serif;
}

p {
  color: rgb(212, 255, 0);
  font-family: 'Star Wars', sans-serif;
}

label {
  color: rgb(212, 255, 0);
  font-family: 'Star Wars', sans-serif;
}
</style>
