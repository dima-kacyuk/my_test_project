<template>
  <div id="app">
    <h1>{{ message }}</h1>
  </div>
</template>

<script>
import api from '../services/api';

export default {
  name: 'App',
  data() {
    return {
      message: 'Loading...',
    };
  },
  mounted() {
    api.get('/hello')
        .then(response => {
          this.message = response.data.message;
        })
        .catch(error => {
          console.error('Error fetching message:', error);
          this.message = 'Error loading message.';
        });
  },
};
</script>

<style>
/* Ваши стили */
</style>
