<template>

  <div v-if="currentPersonne" class="text-center border-dark bg-dark list-group-item mt-3" style="width: 18rem;">
    <h5 class="text-center text-warning">Modifier/Supprimer</h5>
    <input type="text" class="border-dark shadow-lg list-group-item mt-3" id="id" v-model="currentPersonne.id" disabled />
    <input type="text" class="border-dark shadow-lg list-group-item mt-3" id="name" v-model="currentPersonne.name" />
    <input type="text" class="border-dark shadow-lg list-group-item mt-3" id="surname" v-model="currentPersonne.surname" />
    <input type="text" class="border-dark shadow-lg list-group-item mt-3" id="phone" v-model="currentPersonne.phone" />
    <input type="text" class="border-dark shadow-lg list-group-item mt-3" id="city" v-model="currentPersonne.city" />
    
    <!-- A INCLURE DANS LE FORM -->
    <button class="mt-3 badge badge-danger mr-2"
    @click="deletePersonne"
    >
    Supprimer
  </button>

  <!-- A INCLURE DANS LE FORM -->
  <button type="submit" class="mt-3 badge badge-success"
  @click="updatePersonne"
  >
  Modifier
</button>
<p>{{ message }}</p>
</div>
</template>

<script>
  import PersonneDataService from "../services/PersonneDataService";

  export default {
    name: "personne",
    data() {
      return {
        currentPersonne: null,
        message: ''
      };
    },
    methods: {
      getPersonne(id) {
      // A COMPLETER
      PersonneDataService.get(id)
      .then(response => {
        this.currentPersonne = response.data;
        console.log(response.data);
      })
      .catch(e => {
        console.log(e);
      })
      
    },

    updatePersonne() {

     PersonneDataService.update(this.currentPersonne)
     .then(response => {
      this.message = 'Personne modifiée avec succès!';
      console.log(response.data);
    })
     .catch(e => {
      console.log(e);
    })  
   },

   deletePersonne() {

     PersonneDataService.delete(this.currentPersonne.id)
     .then(response => {
      this.$router.push({ name: "personnes" });
      console.log(response.data);
    })
     .catch(e => {
      console.log(e);
    })  
   }
 },
 mounted() {
  this.message = '';
  this.getPersonne(this.$route.params.id);
}
};
</script>

<style>
  .edit-form {
    max-width: 300px;
    margin: auto;
  }
</style>
