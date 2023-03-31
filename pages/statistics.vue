<template>
  <div class="main-body">
    <h1 class="text-center font-bold text-5xl">Archive Engine</h1><br>
    <div>
      <NuxtLink to="/">Search</NuxtLink> -
      <NuxtLink to="/usage">How to use (READ ME)</NuxtLink>
      <table class="max-w[100%] w-[100%]">
        <tr>
          <th>Domain</th>
          <th>Total Urls</th>
          <th>Total Failed Requests</th>
          <th>Indexed To</th>
          <th>Indexed From</th>
        </tr>
        <tr v-for="domain in domains" :key="domain.domain">
          <td>{{ domain.domain }}</td>
          <td>{{ domain.totalUrls }}</td>
          <td>{{ domain.totalFailedRequests }}</td>
          <td>{{ domain.indexedTo }}</td>
          <td>{{ domain.indexedFrom }}</td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: "statistics",
  async asyncData(data) {
    let domains;

    await data.$axios.get(`api/statistics`)
        .then(response => {
          domains = response.data.statistics;
        })
        .catch(error => {
          console.log(error);
        });

    return { domains }
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