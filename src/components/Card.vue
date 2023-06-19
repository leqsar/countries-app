<script setup>

</script>

<script>
    export default {
        props: ['country', 'mode'],
    }

</script>

<template>
    <div class="card-wrapper" @click="$emit('cardClick', country)">
        <img :src="country.flags.png" alt="Flag">
        <h2>{{ country.name.common }}</h2>
        <p><b>Population:</b> {{ country.population }}</p>
        <p><b>Region:</b> {{ country.region }}</p>
        <p><b>Capital:</b> {{ country.capital[0] }}</p>
    </div>
</template>

<style scoped lang="sass">

    @import '../input.sass'

    .card-wrapper
        width: 100%
        height: 340px
        border-radius: 10px
        box-shadow: 0 2px 2px 2px v-bind('mode.shadowColor')
        background-color: v-bind('mode.elementColor')
        color: v-bind('mode.fontColor')

        img
            width: 100%
            height: 160px
            border-top-left-radius: 10px
            border-top-right-radius: 10px
            object-fit: cover

        h2
            margin: 25px 30px
            font-size: 18px
            line-height: 18px
            height: 36px

        p
            margin-left: 30px
            


</style>
