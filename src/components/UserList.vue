<template>
    <ul>
      <UserItem
        v-for="(user, index) in users"
        :key="user.id"
        :user="user"
        :index="index"
        @edit="editUser"
        @delete="deleteUser"
      />
    </ul>
  </template>
  
  <script>
  import UserItem from './UserItem.vue';
  
  export default {
    components: {
      UserItem
    },
    props: {
      users: Array
    },
    emits: ['edit', 'delete'],
    methods: {
      editUser(index) {
        this.$emit('edit', index);
      },
      deleteUser(index) {
        this.$emit('delete', index);
      }
    }
  };
  </script>
  