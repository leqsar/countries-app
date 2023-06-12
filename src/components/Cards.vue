<script setup>
import Card from './Card.vue'
</script>

<script>

    export default {
        data() {
            return {
                countries: []
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
    <div class="cards-wrapper">
        <Card 
            v-for="country in countries" 
            :key="country.name"
            :country="country"
        />
    </div>
</template>

<style scoped lang="sass">

    @import '../input.sass'

    .cards-wrapper
        display: grid
        grid-template-columns: repeat(4, 265px)
        justify-content: space-between
        row-gap: 75px
        width: 100%
        margin-top: 50px
        padding: 0 80px
        box-sizing: border-box

</style>
