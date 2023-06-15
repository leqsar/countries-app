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
        queryString: '',
        isOpen: false,
        countries: [],
        filteredCountries: [],
        searchResults: [],
        showDetails: false,
        chosenCountry: {},
        modeStatus: 'light',
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
      },
      showBorderDetails(countryName) {
        this.chosenCountry = this.countries.filter((country) => {
          return country.name.common===countryName
        })[0]
      },
      setMode() {
        console.log(this.modeStatus)
        this.modeStatus = this.modeStatus === 'light' ? 'dark' : 'light'
      },
      showHome(){
        this.showDetails = false
        this.setSearchQuery('')
      },
      setSearchQuery(searchQuery) {
        this.queryString = searchQuery
      }
    },
    watch: {
      filter(newRegion) {
        if(newRegion !== '') {
          this.filteredCountries =  this.countries.filter((country) => {
            return country.region===newRegion
          })
        }
      },
      queryString(newValue) {
        const editedString = newValue.toLowerCase()
        this.searchResults =  this.countries.filter((country) => {
          return country.name.common.toLowerCase()===editedString
        })
      },
    },
    computed: {
      displayedCountries() {
        if(this.searchResults.length > 0) {
          if(this.filteredCountries.length > 0) {
            return this.filteredCountries
          }
          return this.searchResults
        }
        if(this.filteredCountries.length > 0) {
          return this.filteredCountries
        }
        return this.countries
      },
      mode() {
        if(this.modeStatus === 'dark') {
          return {
            nextStatus: 'Light',
            backColor: 'hsl(207, 26%, 17%)',
            fontColor: 'hsl(0, 0%, 100%)',
            elementColor: 'hsl(209, 23%, 22%)'
          }
        } 
        return {
          nextStatus: 'Dark',
          backColor: 'hsl(0, 0%, 98%)',
          fontColor: 'hsl(200, 15%, 8%)',
          elementColor: 'hsl(0, 0%, 100%)'
        }
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
  <Header :mode="mode" @switch-mode="setMode"/>
  <FilterBlock 
    :filter="filter" 
    :isOpen="isOpen"
    :mode="mode"
    v-if="!showDetails"
    @set-filter="setFilter" 
    @open-menu="openMenu"
    @set-search-query="setSearchQuery"
  />
  <Cards 
    :displayedCountries="displayedCountries"
    :mode="mode"
    v-if="!showDetails"
    @open-details="openDetails" 
  />
  <Country 
    :country="chosenCountry" 
    :countries="countries"
    :mode="mode"
    v-if="showDetails"
    @show-home="showHome"
    @show-border-details="showBorderDetails"
  />
</template>

<style scoped lang="sass">
  @import './input.sass'

</style>
