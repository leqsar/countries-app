<script setup>
import Header from './components/Header.vue'
import FilterBlock from './components/FilterBlock.vue'
import Cards from './components/Cards.vue'
import Country from './components/Country.vue'
</script>

<script>

  export default {
    data() {
      return {
        filter: 'Filter by Region',
        isOpen: false,
        countries: [],
        filteredCountries: [],
        showDetails: false,
        chosenCountry: {}
      }
    },
    methods: {
      setFilter(region) {
        this.filter=region
        this.isOpen=false
      },
      openMenu() {
        this.isOpen = !this.isOpen
      },
      openDetails(country){
        this.chosenCountry = country
        this.showDetails = true
        console.log(country);
      },
      showBorderDetails(countryName) {
        this.chosenCountry = this.countries.filter((country) => {
          return country.name.common===countryName
        })[0]
      },
      showHome(){
        this.showDetails = false
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
      const response = await fetch('https://restcountries.com/v3.1/all?fields=name,flags,capital,population,cca3,region,nativeName,subregion,currencies,languages,tld,borders')
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
    v-if="!showDetails"
  />
  <Cards :displayedCountries="displayedCountries" @open-details="openDetails" v-if="!showDetails"/>
  <Country 
    :country="chosenCountry" 
    :countries="countries" 
    v-if="showDetails"
    @show-home="showHome"
    @show-border-details="showBorderDetails"
  />
</template>

<style scoped>

</style>
