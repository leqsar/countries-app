<script setup>
</script>

<script>
    export default {
        props: ['mode'],
    }

</script>

<template>
    <header>
        <h1>Where in the world?</h1>
        <div class="mode-switcher" @click="$emit('switchMode')">
            <img v-show="mode.nextStatus==='Dark'" class="dark-mode-icon" src="../assets/moon.svg" alt="Dark mode icon">
            <img v-show="mode.nextStatus==='Light'" class="light-mode-icon" src="../assets/sunr.svg" alt="Dark mode icon">
            <p>{{mode.nextStatus}} mode</p>
        </div>
    </header>
</template>

<style scoped lang="sass">

@import '../input.sass'

header
    width: 100%
    height: 80px
    display: flex
    align-items: center
    justify-content: space-between
    color: v-bind('mode.fontColor')
    background-color: v-bind('mode.elementColor')
    padding: 0 80px
    box-sizing: border-box
    box-shadow: 0 4px v-bind('mode.shadowColor')

    @media screen and (max-width: 400px) 
        padding: 0 20px

        h1
            font-size: 20px
        

    .mode-switcher
        display: flex
        font-weight: 600
        gap: 10px

        @media screen and (max-width: 400px) 
            font-size: $homepageFont
            gap: 5px

        &:hover
            cursor: pointer

        .dark-mode-icon,
        .light-mode-icon
            width: 22px
            height: 22px

            @media screen and (max-width: 400px) 
                width: 18px
                height: 18px
</style>
