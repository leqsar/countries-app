<script setup>
import Card from './Card.vue'
</script>

<template>
    <div class="cards-wrapper">
        <Card v-for="n in 10" :key="n"/>
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
