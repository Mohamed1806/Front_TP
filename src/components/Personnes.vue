<template>
  <div class="card shadow-lg bg-body rounded border-dark" style="width: 25rem;">
    <ul class="list-group list-group-flush"> 
      <h5 class=" border-dark text-warning bg-dark text-center list-group-item"> Liste de personnes
      </h5>
      <li class="border-dark list-group-item"
      :class="{ active: id == currentIndex }"
      v-for="(personne, id) in personnes"
      :key="id"
      @click="setActivePersonne(personne, id)">

      {{ personne.name }} {{ personne.surname }}

    </li>

  </ul>
</div>

<div v-if="currentPersonne" class= "card border-dark shadow-lg mt-3 p-3 " style="width: 25rem">
  <ul>
    <li >Prenom: {{ currentPersonne.name }} </li>
    <li> Nom: {{ currentPersonne.surname }}</li>
    <li> Tel: {{ currentPersonne.phone }}</li>
    <li> Ville: {{ currentPersonne.city }}</li>
  </ul>
  <router-link :to="'/personnes/' + currentPersonne.id" class="badge badge-dark text-warning">Modifier</router-link>
</div>
<div v-else>
  <br />
  <p>Cliquez sur une des personnes pour afficher les détails.</p>
</div>

</template>

<script>
  import PersonneDataService from "../services/PersonneDataService";

  export default {
    name: "personnes",
    data() {
      return {
        personnes: [],
        currentPersonne: null,
        currentIndex: -1,
      };
    },
    methods: {
      getPersonnes() {
        PersonneDataService.getAll()
        .then(response => {
          this.personnes = response.data;
          console.log(response.data);
        })
        .catch(e => {
          console.log(e);
        });
      },

      setActivePersonne(personne, index) {
        this.currentPersonne = personne;
        this.currentIndex = personne ? index : -1;
      },
    },
    mounted() {
      this.getPersonnes();
    }
  };
</script>
