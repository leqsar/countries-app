<script setup>
import Header from './components/Header.vue'
import FilterBlock from './components/FilterBlock.vue'
import Cards from './components/Cards.vue'
</script>

<script>

  export default {
    data() {
      return {
        filter: 'Filter by Region',
        isOpen: false,
        countries: [],
        filteredCountries: []
      }
    },
    methods: {
      setFilter(region) {
        this.filter=region
        this.isOpen=false
      },
      openMenu() {
        this.isOpen = !this.isOpen
      }
    },
    watch: {
      filter(newRegion) {
        this.filteredCountries =  this.countries.filter((country) => {
          return country.region===newRegion
        })
      }
    },
    computed: {
      displayedCountries() {
        if(this.filteredCountries.length > 0) {
          return this.filteredCountries
        }
        return this.countries
      }
    },
    async mounted() {
      const response = await fetch('https://restcountries.com/v3.1/all?fields=name,flags,capital,population,alpha3Code,region')
      const countries = await response.json()
      this.countries = countries
    },
  }

</script>

<template>
  <Header />
  <FilterBlock 
    :filter="filter" 
    :isOpen="isOpen" 
    @set-filter="setFilter" 
    @open-menu="openMenu"
  />
  <Cards :displayedCountries="displayedCountries"/>
</template>

<style scoped>

</style>
