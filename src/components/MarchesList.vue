<template>
    <div class="marches-list">
        <div class="data">
            <table class="ui celled table">
                <thead>
                    <tr>
                        <th style="width : 20px; text-align:center;">#</th>
                        <th>Nom</th>
                        <th>Emplacement</th>
                        <th>Nbre de hangars</th>
                        <th>Heure ouverture</th>
                        <th>Heure fermeture</th>
                        <th>Catégorie de Produits</th>
                        <th style="width : 200px;">Actions</th>
                    </tr>
                </thead>
                <tbody>
                    <OneMarche 
                    v-for="marche in marches"
                    :key="marche.id"
                    :marche="marche"
                    @onDelete="onDelete"
                    />
                </tbody>
            </table>
        </div>
    </div>
  </template>
  
  <script>
  import OneMarche from "./OneMarche";
  export default {
    name : "MarchesList",
    components: {
        OneMarche
    },
    props:{
        marches: {
            type: Array
        }
    },
    methods:{
        onDelete(id){
            //window.console.log("marché list deleted " + id);
            this.$emit("onDelete", id);
        }
    }
  }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>

  </style>
  