<template>
    <tr>
        <td>{{marche.id}}</td>
        <td>{{marche.nom}}</td>
        <td>{{marche.emplacement}}</td>
        <td>{{marche.nbre_hangars}}</td>
        <td>{{marche.heure_ouverture}}</td>
        <td>{{marche.heure_fermeture}}</td>
        <td>{{marche.categorie_produit}}</td>
        <td>
            <button class="mini ui blue button">Modifier</button>
            <button class="mini ui red button" @click="onDelete">Supprimmer</button>
        </td>
    </tr>
  </template>
  
  <script>
  export default {
    name : "OneMarche",
    props:{
      marche:{
        type:Object
      }
    },
    methods:{
      onDelete(){
        //window.console.log("marché deleted " + this.marche.id);
        this.$emit("onDelete", this.marche.id);
      }
    }
  }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>

  </style>
  