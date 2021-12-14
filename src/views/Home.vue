<template>
  <div class="container mx-auto w-3/4 flex justify-center h-screen">

    <div class="loader w-14 flex items-center" v-if="loading">
      <img :src="loadingImage" alt="" >
      <h3 class="text-xl font-semibold text-gray-600">Fetching</h3>
    </div>

    <div class="mt-5" v-else>
      <Data :text="title" :dataDate="dataDate"/>

      <DataBox :stats="stats"/>

      <CountrySelect :countries="countries" @get-country="getCountryData"/>

      <button  @click="clearCountry" v-if="stats.Country" class="bg-green-700 text-white rounded p-3 mt-10 focus:outline-none hover:bg-green-600">
        Clear Country
      </button>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Data from '@/components/Data'
import DataBox from '@/components/DataBox'
import CountrySelect from '@/components/CountrySelect'



export default {
  name: 'Home',
  components: {
    Data,
    DataBox,
    CountrySelect

  },
  data(){
    return{
      loading: true,
      countries: [],
      title: 'Global',
      dataDate: '',
      stats: {},
      loadingImage: require('../assets/Double Ring-1s-200px.gif')

    }
  },
  methods:{
    async fetchData(){
      let res = await fetch('https://api.covid19api.com/summary');

      let data = await res.json();

      return data

    },
    getCountryData(country){
      this.stats = country
      this.title = country.Country
    },
    async clearCountry(){
      this.loading = true

      let data = await this.fetchData()
      this.title = 'Global'
      this.stats = data.Global
      this.loading = false
    }
  },
  async created(){
    let data = await this.fetchData();

    this.countries = data.Countries;
    this.dataDate = data.Date;
    this.stats = data.Global;
    this.loading = !this.loading;
  }
}
</script>
