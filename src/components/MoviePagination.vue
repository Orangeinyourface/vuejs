<template>
    <div>
      <v-btn @click="previousPage">Page précédente</v-btn>
      <v-btn @click="nextPage">Page suivante</v-btn>
    </div>
  </template>
  
  <script>
  export default {
    name: 'MoviePagination',
    props: {
      currentPage: {
        type: Number,
        required: true
      }
    },
    methods: {
      nextPage() {
        this.$emit('change-page', this.currentPage + 1);
      },
      previousPage() {
        if (this.currentPage > 1) {
          this.$emit('change-page', this.currentPage - 1);
        }
      }
    }
  }
  </script>