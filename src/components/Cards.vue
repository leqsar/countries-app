<script setup>
import { nextTick } from 'vue'
import Card from './Card.vue'
</script>

<script>
    export default {
        props: ['displayedCountries', 'mode'],
    }
</script>

<template >
    <div class="cards-wrapper">
        <Card 
            v-for="country in displayedCountries" 
            :key="country.name"
            :country="country"
            :mode="mode"
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

        @media screen and (max-width: 400px) 
            width: 90%
            margin: 50px auto
            padding: 0 5%
            row-gap: 40px
            grid-template-columns: 1fr
            
        .loader
            position: absolute
            top: 15px
            left: 500px
            width: 20px
            height: 20px
            border-radius: 10px
            border-top: 2px solid v-bind('mode.fontColor')
            border-left: 2px solid v-bind('mode.fontColor')
            animation: loading 1.25s linear infinite

            @keyframes loading 
                0% 
                    transform: rotate(0deg)
                    
                33% 
                    transform: rotate(120deg)
                
                66% 
                    transform: rotate(240deg)
                
                100% 
                    transform: rotate(360deg)
        

</style>
