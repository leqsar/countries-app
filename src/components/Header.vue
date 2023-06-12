<script setup>

</script>

<template>
    <header>
        <h1>Where in the world?</h1>
        <div class="mode-switcher">
            <img class="dark-mode-icon" src="../assets/moon.svg" alt="Dark mode icon">
            <p>Dark mode</p>
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
    color: $lightModeText
    padding: 0 80px
    box-sizing: border-box
    background-color: $lightModeElements
    box-shadow: 0 4px $shadowColor

    .mode-switcher
        display: flex
        font-weight: 600
        gap: 10px

        .dark-mode-icon
            width: 22px
            height: 22px 

</style>
