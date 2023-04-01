<template>
  <div class="main-body">
    <h1 class="text-center font-bold text-5xl">Archive Engine</h1><br>
    <div>
      <NuxtLink to="/usage">How to use (READ ME)</NuxtLink>
      -
      <NuxtLink to="/statistics">Statistics</NuxtLink>
      <input type="text" id="search" class="search-box" v-on:keydown="keydown"><br><br>
      <input type="button" value="Search" v-on:click="searchClicked" class="search-button"><br><br>
      <div v-if="searching" class="loader ml-auto mr-auto"></div>
      <div v-if="urls !== null">
        <p v-if="urls.length === 0">No results</p>
        <div v-else>
          <input type="button" id="back" class="back" value="Back" v-on:click="back">
          <label>Page: {{ page }}</label>
          <input type="button" id="next" class="next" value="Next" v-on:click="next"><br><br>
          <table class="max-w[100%] w-[100%]">
            <tr>
              <th id="url" v-on:click="sortBy('url')">URL
                {{ sort === 'url' ? (this.ascending ? '&#8593;' : '&#8595;') : '' }}
              </th>
              <th id="timestamp" v-on:click="sortBy('timestamp')">Timestamp
                {{ sort === 'timestamp' ? (this.ascending ? '&#8593;' : '&#8595;') : '' }}
              </th>
              <th id="mimeType" v-on:click="sortBy('mimeType')">Mime Type
                {{ sort === 'mimeType' ? (this.ascending ? '&#8593;' : '&#8595;') : '' }}
              </th>
              <th id="statusCode" v-on:click="sortBy('statusCode')">Status Code
                {{ sort === 'statusCode' ? (this.ascending ? '&#8593;' : '&#8595;') : '' }}
              </th>
            </tr>
            <tr v-for="url in urls">
              <td>
                <a target="_blank" :href="`https://web.archive.org/web/${url.timestamp}/${url.url}`">{{ url.url }}</a>
              </td>
              <td>{{ url.timestamp }}</td>
              <td>{{ url.mimeType }}</td>
              <td>{{ url.statusCode }}</td>
            </tr>
          </table>
          <br>
          <input type="button" id="back" class="back" value="Back" v-on:click="back">
          <label>Page: {{ page }}</label>
          <input type="button" id="next" class="next" value="Next" v-on:click="next">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "index",
  data() {
    return {
      urls: null,
      page: 0,
      searching: false,
      sort: 'timestamp',
      ascending: false
    }
  },
  methods: {
    keydown: async function (key) {
      if (key.key === "Enter") {
        await this.searchClicked();
      }
    },
    searchClicked: async function () {
      this.page = 0;
      await this.search();
    },
    search: async function () {
      const search = document.getElementById('search').value;

      if (search === "") return;

      this.searching = true;

      this.$axios.get(`api/search?query=${search}&page=${this.page}&sortBy=${this.sort}&ascending=${this.ascending}`)
          .then(response => {
            this.urls = response.data;
          })
          .catch(error => {
            console.log(error);
          }).finally(() => {
        this.searching = false;
      });
    },
    next: async function () {
      if (this.urls.length < 50 || this.searching) return;
      this.page++;
      await this.search();
    },
    back: async function () {
      if (this.page === 0 || this.searching) return;
      this.page--;
      await this.search();
    },
    sortBy: async function (sort) {
      if (this.sort === sort) {
        this.ascending = !this.ascending;
      } else {
        this.ascending = true;
        this.sort = sort;
      }
      await this.search();
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

.search-box {
  width: 100%;
  height: 50px;
  font-size: 20px;
  border: 1px solid #000;
  border-radius: 5px;
  padding: 0 10px;
}

.search-button {
  width: 100%;
  height: 50px;
  font-size: 20px;
  border: 1px solid #000;
  border-radius: 5px;
  padding: 0 10px;
  background-color: #000;
  color: #fff;
  cursor: pointer;
}

.back {
  width: 50px;
  height: 25px;
  border: 1px solid #000;
  border-radius: 5px;
  background-color: #000;
  color: #fff;
  cursor: pointer;
}

.next {
  width: 50px;
  height: 25px;
  border: 1px solid #000;
  border-radius: 5px;
  background-color: #000;
  color: #fff;
  cursor: pointer;
}

.loader {
  border: 8px solid #f3f3f3;
  border-top: 8px solid #000000;
  border-radius: 50%;
  width: 60px;
  height: 60px;
  animation: spin 1.5s linear infinite;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>