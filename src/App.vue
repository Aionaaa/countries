<template lang="html">
  <div>
    <h1>Countries</h1>
    <div class="main-container">
    <countries-list :countries="countries"></countries-list>
    <country-detail :country="selectedCountry"></country-detail>
    <div id="filterInput">
      <h3>Filter Countries</h3>
      <select id="text" v-model="filteredCountries">
        <option v-for="country in countries" :value="country">{{country.name}}</option>
      </select>
    </div>
    <select class="country" v-for="country in countries">
      <h3>{{country.name}}</h3>
      <p>{{country.capital}}</p>
      <p>{{country.population}}</p>
      <img id="flagImg" :src="country.flag">
    </select>
  </div>
</div>
</template>

<script>
import CountriesList from './components/CountriesList.vue';
import CountryDetail from './components/CountryDetail.vue';
import {eventBus} from './main.js';

export default {
  name: 'app',
  data(){
    return {
      countries: [],
      selectedCountry: null
    };
  },
  mounted(){
    eventBus.$on("country-selected", (country) => {
      this.selectedCountry = country;
    })

    eventBus.$on("filteredCountries", (name) => {
      this.countries.filter(country => this.country.name)
    })

    fetch('https://restcountries.eu/rest/v2/all')
    .then(res => res.json())
    .then(countries => this.countries = countries)
  },
  components: {
    "countries-list": CountriesList,
    "country-detail": CountryDetail
  }
}
</script>

<style lang="css" scoped>

.main-container {
  display: flex;
  justify-content: space-between;
}
</style>
