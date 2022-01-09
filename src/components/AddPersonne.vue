<template>
  <div class="card bg-dark shadow-lg p-3 bg-body rounded border-dark" style="width: 18rem;">
    <div v-if="!submitted">
      <h5 class="text-center  text-warning">Entrez les informations</h5>


      <input type="text" placeholder="Id" class="container mt-3" id="id" required v-model="personne.id" name="id" disabled/>
      <input type="text" placeholder="Prenom" class="container mt-3" id="name" required v-model="personne.name" name="name"/>
      <input type="text" placeholder="Nom" class="container mt-3" id="surname" required v-model="personne.surname" name="surname"/>
      <input type="text" placeholder="Tel" class="container mt-3" id="phone" required v-model="personne.phone" name="phone"/>
      <input type="text" placeholder="Ville" class="container mt-3" id="city" required v-model="personne.city" name="city"/>


      <button type="submit" class="container border-dark mt-3 badge-success" @click="creerPersonne"> Ajouter</button>
      
    </div>

    <div v-else>
      <h4>Personne ajoutée avec succès!</h4>
      
    </div>
  </div>
</template>

<script>
  import PersonneDataService from "../services/PersonneDataService";

  export default {
    name: "add-personne",
    data() {
      return {
        personne: {
          id: null,
          name: "",
          surname: "",
          phone: "",
          city: ""
        },
        submitted: false
      };
    },
    methods: {
      creerPersonne() {
        var data = {
          id: this.personne.id,
          name: this.personne.name,
          surname: this.personne.surname,
          phone: this.personne.phone,
          city: this.personne.city,

        };

        PersonneDataService.create(data)
        .then(response => {
          this.$router.push({ name: "personnes" });
          this.message = 'Personne créé avec succès!';
          console.log(response.data);
        })
        .catch(e => {
          console.log(e);
        })    
      },

      resetForm() {
        this.submitted = false;
        this.personne = {};
      }
    }

  };
</script>

<style>
  .submit-form {
    max-width: 300px;
    margin: auto;
  }
</style>
