<script setup>

</script>

<script>
    export default {
        props: ['imgSrc', 'name', 'population', 'region', 'capital']
    }

</script>

<template>
    <div class="card-wrapper">
        <img src="imgSrc" alt="Flag">
        <h2>{{ name }}</h2>
        <p><b>Population</b>: {{ population }}</p>
        <p><b>Region</b>: {{ region }}</p>
        <p><b>Capital</b>: {{ capital }}</p>
    </div>
</template>

<style scoped lang="sass">

    @import '../input.sass'

    .card-wrapper
        width: 100%
        height: 340px
        border-radius: 10px
        box-shadow: 0 2px 2px 2px $shadowColor

        img
            width: 100%
            height: 160px

        h2
            margin: 30px 30px

        p
            margin-left: 30px
            margin-top: 10px

        p:first-of-type
            margin-top: 0


</style>
