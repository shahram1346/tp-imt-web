<template>
  <div v-if="currentPersonne">
    <div class="col-sm-6">
      <label for="id" class="form-label">Identifiant</label>
      <input type="text" class="form-control" id="id" v-model="currentPersonne.id" name="id">
    </div>  
    <div class="col-sm-6">
      <label for="name" class="form-label">Name</label>
      <input type="text" class="form-control" id="name" v-model="currentPersonne.name" name="name">
    </div>  
    <div class="col-sm-6">
      <label for="surname" class="form-label">Surname</label>
      <input type="text" class="form-control" id="surname" v-model="currentPersonne.surname" name="surname">
    </div>  

    <div class="col-sm-6">
      <label for="phone" class="form-label">Phone</label>
      <input type="text" class="form-control" id="phone" v-model="currentPersonne.phone" name="phone">
    </div>  

    <div class="col-sm-6">
      <label for="city" class="form-label">City</label>
      <input type="text" class="form-control" id="city" v-model="currentPersonne.city" name="city">
    </div>  

        
    <!-- A INCLURE DANS LE FORM -->
    <button class="badge badge-danger mr-2"
      @click="deletePersonne"
    >
      Supprimer
    </button>

    <!-- A INCLURE DANS LE FORM -->
    <button type="submit" class="badge badge-success"
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
      PersonneDataService.get(id)
        .then(response => {
          this.currentPersonne = response.data;
          console.log(response.data);
        })
        .catch(e => {
          console.log(e);
        });
    },

    updatePersonne() {
      PersonneDataService.update(this.currentPersonne)
      .then(response => {
          this.currentPersonne = response.data;
          console.log(response.data);
        })
        .catch(e => {
          console.log(e);
        });
      
    },

    deletePersonne() {
      PersonneDataService.delete(this.currentPersonne.id)
      .then(response => {
          this.currentPersonne = response.data;
          console.log(response.data);
        })
        .catch(e => {
          console.log(e);
        });
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
