<template>
  <div id="app">
    <vs-table :data="data" :sst="true" pagination description :total="count" max-items="20" @change-page="handleChangePage">
      <template slot="thead">
        <vs-th
          key="name"
          sort-key="name"
        >name</vs-th>
      </template>
      <template slot-scope="{ data }">
        <vs-tr :data="tr" :key="indextr" v-for="(tr, indextr) in data">
          <vs-td
            :data="data[indextr].name"
          >{{ data[indextr].name }}</vs-td>
        </vs-tr>
      </template>
    </vs-table>
  </div>
</template>

<script>
export default {
  data() {
    return { data: [
    ] };
  },
  mounted() {
    fetch('https://pokeapi.co/api/v2/pokemon').then(response => response.json() )
    .then(response => {
      this.data = response.results
      this.count = response.count
    })
  },
  methods: {
    handleChangePage(page) {
      fetch('https://pokeapi.co/api/v2/pokemon?offset=' + 20 * (page - 1) + 'limit=20' ).then(response => response.json() )
        .then(response => {
          this.data = response.results
          this.count = response.count
        })
    }
  }
};
</script>