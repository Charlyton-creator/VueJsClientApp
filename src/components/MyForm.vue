<template>
    <div class="my-form">
        <form class="ui form">
            <h4 class="ui dividing header">Informations sur le marché à ajouter</h4>
            <div class="field">
                <label>Identification</label>
                <div class="two fields">
                <div class="field">
                    <input type="text" name="nom" placeholder="Nom du marché" @change="handleChange" :value="form.nom">
                </div>
                <div class="field">
                    <input type="text" name="emplacement" placeholder="Lieu ou Emplacement" @change="handleChange"
                    :value="form.emplacement"
                    >
                </div>
                </div>
            </div>
            <div class="field">
                <label>Heures</label>
                <div class="two fields">
                <div class="field">
                    <input type="text" name="heure_ouverture" placeholder="Heure d'ouverture exp 80h30" @change="handleChange"
                    :value="form.heure_ouverture"
                    >
                </div>
                <div class="field">
                    <input type="text" name="heure_fermeture" placeholder="Heure de fermeture exp 19h00" @change="handleChange"
                    :value="form.heure_fermeture"
                    >
                </div>
                </div>
            </div>
            <div class="two fields">
                <div class="field">
                <label>Categorie de Produits vendus</label>
                <select class="ui fluid dropdown" name="categorie_produit" @change="handleChange" :value="form.categorie_produit" >
                        <option value="MEDECINE">MEDECINE</option>
                        <option value="TECHNOLOGIE">TECHNOLOGIE</option>
                        <option value="COSMETIQUE">COSMETIQUE</option>
                        <option value="ALIMENTATION">ALIMENTATION</option>
                    </select>
                </div>
                <div class="field">
                    <label>Nombre de hangars du marché</label>
                    <input type="number" name="nbre_hangars" id="" placeholder="3" @change="handleChange" :value="form.nbre_hangars">
                </div>
            </div> 
            <div class="ui button primary" tabindex="0" @click="onFormSubmit">Enregistrer le marché</div>
        </form>
    </div>
  </template>
  
  <script>
  export default {
    name : "MyForm",
    props : {
        form: {
            type: Object
        }
    },
    methods: {
        handleChange(event){
            const {name, value} = event.target;
            let form = this.form;
            form[name] = value;
            //this.form = form;
        },
        onFormSubmit(e){
            //
            e.preventDefault();
            //
            if(this.formValidation()){
                //window.console.log("ready to submit");
                this.$emit("onFormSubmit", this.form);
                //clear form field
                this.clearFormFields();
            }
        },
        formValidation(){
            //nom du marché requis
            if(document.getElementsByName("nom")[0].value === " "){
                alert("Vous devez spécifier un nom de Marché");
                return false;
            }
            //Son emplacement
            if(document.getElementsByName("emplacement")[0].value === " "){
                alert("Veuillez spécifier l'amplacement");
                return false;
            }
            //Heure_ouverture
            if(document.getElementsByName("heure_ouverture")[0].value === " "){
                alert("Vous devez une heure du debut l'ouverture du marcé");
                return false;
            }
            //heure_fermeture
            if(document.getElementsByName("heure_fermeture")[0].value === " "){
                alert("Vous devez spécifier une heure pour la fermeture");
                return false;
            }
            return true;
        },
        clearFormFields(){
            /*
            this.form.nom = "";
            this.form.emplacement = "";
            this.form.nbre_hangars = "";
            this.form.heure_ouverture = "";
            this.form.heure_fermeture = "";
            this.form.categorie_produit = "";
            this.form.isEdit = false;
            */
            //clear form field
            document.querySelector('.form').reset();
        }
    }
  }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>

  </style>
  