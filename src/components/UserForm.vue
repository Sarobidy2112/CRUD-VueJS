<template>
    <form @submit.prevent="handleSubmit">
      <input
        type="text"
        v-model="newUser.nom"
        placeholder="Nom"
        required
      />
      <input
        type="text"
        v-model="newUser.prenom"
        placeholder="Prénom"
        required
      />
      <input
        type="email"
        v-model="newUser.email"
        placeholder="Email"
        required
      />
      <input
        type="text"
        v-model="newUser.adresse"
        placeholder="Adresse"
        required
      />
      <button type="submit">
        {{ isEditing ? "Modifier" : "Ajouter" }}
      </button>
    </form>
  </template>
  
  <script>
  export default {
    props: {
      newUser: Object,
      isEditing: Boolean
    },
    emits: ['submit', 'reset'],
    methods: {
      handleSubmit() {
        this.$emit('submit');
      }
    }
  };
  </script>
  