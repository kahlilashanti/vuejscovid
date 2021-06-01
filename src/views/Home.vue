<template>
  <main v-if="!loading">Show Data</main>
  <main class="flex flex-col align-center justify-center text-center" v-else>
    <div class="text-gray-500 text-3xl mt-10 mb-6">Fetching Latest Data</div>
    <img :src="loadingImage" class="w-24 m-auto" alt="" />
  </main>
</template>

<script>
export default {
  name: "Home",
  components: {},
  data() {
    return {
      loading: true,
      title: "Global",
      dataDate: "",
      stats: {},
      countries: [],
      loadingImage: require("../assets/big-head.gif"),
    };
  },
  methods: {
    async fetchCovidData() {
      const res = await fetch("https://api.covid19api.com/summary");
      const data = await res.json();
      return data;
    },
  },
  async created() {
    // console.log(123);
    const data = await this.fetchCovidData();
    // console.log(data);
    // assign values to the empty elements in lines 13-15
    this.dataDate = data.Date;
    this.stats = data.Global;
    this.countries = data.Countries;
    this.loading = false;
  },
};
</script>
