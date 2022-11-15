<template>
  <div class="submit-form">
    <div v-if="!submitted">
      <h4>Ajouter une personne</h4>
    
      <div class="col-sm-6">
        <label for="id" class="form-label">Identifiant</label>
        <input type="text" class="form-control" id="id" name="id" v-model="this.personne.id">
      </div>  
    
      <div class="col-sm-6">
        <label for="name" class="form-label">Name</label>
        <input type="text" class="form-control" id="name" name="name" v-model="this.personne.name">
      </div>  
      <div class="col-sm-6">
        <label for="surname" class="form-label">Surname</label>
        <input type="text" class="form-control" id="surname" name="surname" v-model="this.personne.surname">
      </div>  

      <div class="col-sm-6">
        <label for="phone" class="form-label">Phone</label>
        <input type="text" class="form-control" id="phone" name="phone" v-model="this.personne.phone">
      </div>  

      <div class="col-sm-6">
        <label for="city" class="form-label">City</label>
        <input type="text" class="form-control" id="city" name="city" v-model="this.personne.city">
      </div>  
    
<br/>
<div class="col-sm-6">

      <button @click="creerPersonne" class="btn btn-success">Ajouter</button>
    </div>
    </div>

    <div v-else>
      <h4>Personne ajoutée avec succès!</h4>
      <button class="btn btn-success" @click="resetForm">Ajouter une nouvelle personne</button>
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
          this.submitted = true;
          console.log(response.data);
        })
        .catch(e => {
          console.log(e);
        });
      
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
  /*max-width: 300px;*/
  margin: auto;
}
</style>
