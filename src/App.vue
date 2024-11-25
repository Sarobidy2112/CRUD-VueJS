<template>
  <div class="app">
    <h1>CRUD pour Utilisateur</h1>

    <UserForm
      :newUser="newUser"
      :isEditing="isEditing"
      @submit="handleSubmit"
    />

    <UserList
      :users="users"
      @edit="editUser"
      @delete="deleteUser"
    />
  </div>
</template>

<script>
import { reactive, ref } from 'vue';
import UserForm from './components/UserForm.vue';
import UserList from './components/UserList.vue';

export default {
  components: {
    UserForm,
    UserList
  },
  setup() {
    // Données réactives
    const users = reactive([]);
    const newUser = ref({ nom: "", prenom: "", email: "", adresse: "" });
    const isEditing = ref(false);
    const currentIndex = ref(null);

    // Ajouter un utilisateur avec ID auto-généré
    const addUser = () => {
      const id = users.length > 0 ? users[users.length - 1].id + 1 : 1;
      users.push({ id, ...newUser.value });
      resetForm(); // Reinitiale la form après ajout
    };

    // Modifier un utilisateur
    const editUser = (index) => {
      isEditing.value = true;
      currentIndex.value = index;
      newUser.value = { ...users[index] };
    };

    const updateUser = () => {
      users[currentIndex.value] = { ...users[currentIndex.value], ...newUser.value };
      resetForm();
    };

    // Supprimer un utilisateur
    const deleteUser = (index) => {
      users.splice(index, 1);
    };

    // Soumettre le formulaire
    const handleSubmit = () => {
      if (isEditing.value) {
        updateUser();
      } else {
        addUser();
      }
    };

    // Réinitialiser le formulaire
    const resetForm = () => {
      newUser.value = { nom: "", prenom: "", email: "", adresse: "" };
      isEditing.value = false;
      currentIndex.value = null;
    };

    return {
      users,
      newUser,
      isEditing,
      addUser,
      editUser,
      deleteUser,
      handleSubmit,
    };
  }
};
</script>
