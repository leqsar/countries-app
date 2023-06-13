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
        chosenCountry: {},
        modeStatus: 'light'
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
    @set-filter="setFilter" 
    @open-menu="openMenu"
    v-if="!showDetails"
  />
  <Cards 
    :displayedCountries="displayedCountries"
    :mode="mode"
    @open-details="openDetails" 
    v-if="!showDetails"
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
