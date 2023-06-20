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
      setNameFilter(searchQuery) {
        this.queryString = searchQuery
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
        this.modeStatus = this.modeStatus === 'light' ? 'dark' : 'light'
      },
      showHome(){
        this.showDetails = false
        this.queryString = ''
        this.searchResults = ''
      },
      reset() {
        this.filter='Filter by Region'
        this.isOpen=false
        this.filteredCountries=[]
        this.searchResults=[]
      }
    },
    watch: {
      filter(newRegion) {
        if(newRegion !== '') {
          if(this.searchResults.length > 0) {
            this.filteredCountries =  this.searchResults.filter((country) => {
              return country.region===newRegion
            })
          } else {
            this.filteredCountries =  this.countries.filter((country) => {
              return country.region===newRegion
            })
          }
        }
      },
      queryString(newValue) {
        if(newValue !== '') {
          const regex = new RegExp(newValue, 'i');
          if(this.filteredCountries.length > 0) {
            this.searchResults = this.filteredCountries.filter(element => regex.test(element.name.common));
          } else {
            this.searchResults = this.countries.filter(element => regex.test(element.name.common));
          }
        } else {
          this.searchResults=[]
        }
      }
    },
    computed: {
      displayedCountries() {
        if(this.searchResults.length > 0 && this.filteredCountries.length > 0) {
          return this.filteredCountries.filter(x => this.searchResults.includes(x))
        }
        if(this.searchResults.length > 0) {
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
            elementColor: 'hsl(209, 23%, 22%)',
            shadowColor: '#1f2c35'
          }
        }
        if(this.modeStatus === 'light') {
          return {
            nextStatus: 'Dark',
            backColor: 'hsl(0, 0%, 98%)',
            fontColor: 'hsl(200, 15%, 8%)',
            elementColor: 'hsl(0, 0%, 100%)',
            shadowColor: '#f2f2f2'
          }
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
  <div class="app-mode-wrapper">
    <div class="app-wrapper">
      <Header 
        :mode="mode" 
        @switch-mode="setMode"
        @go-home="reset"
      />
      <FilterBlock 
        :filter="filter" 
        :isOpen="isOpen"
        :mode="mode"
        v-if="!showDetails"
        @set-filter="setFilter" 
        @filter="setNameFilter"
        @open-menu="openMenu"
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
    </div>
  </div>
</template>

<style scoped lang="sass">
  @import './input.sass'

  .app-mode-wrapper
    width: 100%
    height: 100%
    background-color: v-bind('mode.backColor')

    .app-wrapper
      width: min(100%, 1440px)
      min-height: 100vh
      height: max-content
      margin: 0 auto
    

</style>
