<script setup>
import Card from './Card.vue'
</script>

<script>
    export default {
        props: ['displayedCountries'],
    }
</script>

<template>
    <div class="cards-wrapper">
        <Card 
            v-for="country in displayedCountries" 
            :key="country.name"
            :country="country"
            @card-click="$emit('openDetails', country)"
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
