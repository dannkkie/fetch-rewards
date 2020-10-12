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

        // using proxy because i had CORS issues

        let proxyUrl = 'https://cors-anywhere.herokuapp.com/';
        let targetUrl = 'https://fetch-hiring.s3.amazonaws.com/hiring.json';
        try{
          const response = await fetch(proxyUrl + targetUrl);
          const results = await response.json();
          const filteredResults = results.filter(result => result.name !== null && result.name !== '');
          const sortAlphaNum = (first, second) => first['name'].localeCompare(second['name'], 'en', {numeric: true})
          const sortedList = filteredResults.sort(sortAlphaNum);
          const sortedResultsByListId = sortedList.sort((first, second) => first['listId'] - second['listId']);
          this.results = sortedResultsByListId;
          console.log(this.results)
          } catch(error) {
            console.log(error);
          }
      }
    }
  }
</script>
