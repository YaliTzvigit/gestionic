<!-- eslint-disable vue/multi-word-component-names -->
 
<template>
    <ion-header>
      <ion-toolbar>
        <ion-title>Produits</ion-title>
      </ion-toolbar>
    </ion-header>
  
    <ion-content>
      <ion-list>
        <ion-item v-for="produit in produits" :key="produit.id">
          {{ produit.nom }} - {{ produit.quantite }} en stock - {{ produit.prix }} €
        </ion-item>
      </ion-list>
      <ion-button @click="ajouterProduit">Ajouter un produit</ion-button>
    </ion-content>
  </template>


<script>
import databaseService from '@/services/database';

export default {
  data() {
    return {
      produits: [],
    };
  },
  async mounted() {
    await databaseService.initializeDatabase();
    this.loadProduits();
  },
  methods: {
    async loadProduits() {
      this.produits = await databaseService.getProduits();
    },
    async ajouterProduit() {
      await databaseService.addProduit('Produit test', 10, 25.5);
      this.loadProduits(); // Rafraîchir la liste après ajout
    }
  }
};
</script>
