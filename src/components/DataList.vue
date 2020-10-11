<template>
  <v-container>
    <v-data-table
    :headers="headers"
    :items="item"
    :items-per-page="10"
    class="elevation-1"
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
      results: []
    }),
  }
</script>
