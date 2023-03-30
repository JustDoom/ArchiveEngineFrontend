<template>
  <div class="main-body">
    <h1 class="">Archive Engine</h1>
    <input type="text" id="search">
    <input type="button" value="Search" v-on:click="search">
    <br>
    <table>
      <tr>
        <th>URL</th>
        <th>Timestamp</th>
        <th>Mime Type</th>
        <th>Status Code</th>
      </tr>
      <tr v-for="url in urls">
        <td>{{ url.url }}</td>
        <td>{{ url.timestamp }}</td>
        <td>{{ url.mimeType }}</td>
        <td>{{ url.statusCode }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: "index",
  data() {
    return {
      urls: []
    }
  },
  methods: {
    search: async function () {
      const search = document.getElementById('search').value;

      this.$axios.get(`api/search?query=${search}`)
          .then(response => {
            console.log(response.data);
            this.urls = response.data;
          })
          .catch(error => {
            console.log(error);
          });
    }
  }
}
</script>

<style>
table {
  border-collapse: collapse;
  width: 100%;
}
td, th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}
tr:nth-child(even) {
  background-color: #dddddd;
}
</style>