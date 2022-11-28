<template>
  <div id="App">
    <div class="ui fixed inverted menu vue-color">
      <div class="ui container">
        <a href="#" class="header item">Application Cliente pour L'API SPRING BOOT</a>
      </div>
    </div>

    <div class="ui main container">
      <MyForm :form="form" @onFormSubmit="onFormSubmit"/>
      <TheLoader v-if="loader"/>
      <MarchesList :marches="marches" @onDelete="onDelete"/>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import MyForm from "./components/MyForm"; 
import MarchesList from "./components/MarchesList";
import TheLoader from "./components/TheLoader";
export default {
  name: 'App',
  components: {
    MyForm,
    MarchesList,
    TheLoader
  },
  data(){
    return{
      url: "http://localhost:8080/marches",
      marches : [],
      form: {
        nom: " ",
        emplacement: " ",
        nbre_hangars:  " ",
        heure_ouverture :" ",
        heure_fermeture : " ",
        categorie_produit : " ",
        isEdit: false
      },
      loader:false
    }; 
  },
  methods:{
    getMarches(){
      this.loader = true;
      axios.get(this.url).then(data => {
        this.marches = data.data;
        this.loader = false;
      });
    },
    createMarche(data){
      this.loader = true;

      axios.post(`${this.url}/add`, {
        nom: data.nom,
        emplacement: data.emplacement,
        nbre_hangars: data.nbre_hangars,
        heure_ouverture: data.heure_ouverture,
        heure_fermeture: data.heure_fermeture,
        categorie_produit: data.categorie_produit

      }).then(() =>{
        this.getMarches();
      }).catch(e =>{
        alert(e);
      });
    },
    deleteMarche(id){
      this.loader = true;
      axios.delete(`${this.url}/delete/${id}`).then(() =>{
        this.getMarches();
      }).catch(e =>{alert(e);});
    },
    onDelete(id){
      //window.console.log("app delete" + id);
      this.deleteMarche(id);
    },
    onFormSubmit(data){
      //window.console.log("app onFormSubmit", data);
      if(data.isEdit){
        //edit marché

      }else{
        //create marché
        this.createMarche(data);
      }
    },
  }, 
  created(){
    this.getMarches();
  }
}
</script>

<style>
.vue-color{
  background: #41b883 !important;
}
.main.container{
  margin-top: 60px;
}
.marches-list{
  margin-top: 20px;
}
.data{
  margin-top: 15px;
}
thead tr th{
  background: #e0e0e0 !important;
}
.ui.inverted.dimmer{
  background-color: rgba(255,255,255,0) !important;
}
</style>
