<template>
  <v-container>
    <v-toolbar flat>
      <v-toolbar-title class="font-weight-black">Fetch Rewards exercise - Grouping, Sorting and Filtering</v-toolbar-title>
    </v-toolbar>
    <v-data-table
    :headers="headers"
    :items="results"
    :items-per-page="50"
    group-by="listId"
    class="elevation-8 mt-12"
    >
    </v-data-table>
  </v-container>
</template>

<script>
  export default {
    name: 'DataList',

    data: () => ({
      headers: [
        {
          text: 'ListID',
          align: 'start',
          value: 'listId',
        },
        {
          text: 'Name',
          value: 'name',
        },
      ],

      results: [],
    }),

    created() {
      this.fetchData();
    },

    methods: {
      async fetchData() {
        let proxyUrl = 'https://cors-anywhere.herokuapp.com/';
        let targetUrl = 'https://fetch-hiring.s3.amazonaws.com/hiring.json';
        try{
          const response = await fetch(proxyUrl + targetUrl);
          const results = await response.json();
          const filteredResults = results.filter(result => result.name !== null && result.name !== '');
          const sortedResultsByName = filteredResults.sort((first, second) => first['name'] > second['name']);
          const sortedResultsByListId = sortedResultsByName.sort((first, second) => first['listId'] - second['listId']);
          
        //   const sortedResultsByListId = filteredResults.sort((first, second) => first['listId'] - second['listId']);
        //   const sortedResultsByName = sortedResultsByListId.sort((first, second) => first['name'] > second['name']);

          this.results = sortedResultsByListId;
          console.log(this.results)
          } catch(error) {
            console.log(error);
          }
      }
    }
  }
</script>
