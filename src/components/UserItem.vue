<template>
  <tr>
    <td>{{ user.id }}</td>
    <td>{{ user.nom }}</td>
    <td>{{ user.prenom }}</td>
    <td>{{ user.email }}</td>
    <td>{{ user.adresse }}</td>
    <td>
      <button @click="editUser">Modifier</button>
      <button @click="deleteUser">Supprimer</button>
    </td>
  </tr>
</template>

<script>
export default {
  props: {
    user: Object,
    index: Number
  },
  emits: ['edit', 'delete'],
  methods: {
    editUser() {
      this.$emit('edit', this.index);
    },
    deleteUser() {
      this.$emit('delete', this.index);
    }
  }
};
</script>
