<script setup>
    import CustomSelect from './CustomSelect.vue'
</script>

<script>
    export default {
        data() {
            return {
                searchQuery: '',
                filter: ''
            }
        }
    }

</script>

<template>
    <div class="forms-wrapper">
        <form action="" class="search-form">
            <img class="search-icon" src="../assets/search.svg" alt="Search icon">
            <input type="text" v-model="searchQuery" placeholder="Search for a country...">
        </form>
        <CustomSelect />
    </div>
</template>

<style scoped lang="sass">

    @import '../input.sass'

    .forms-wrapper 
        width: 100%
        display: flex
        justify-content: space-between
        padding: 0 80px
        box-sizing: border-box
        margin-top: 50px

        .search-form
            width: 480px
            height: 60px
            display: flex
            align-items: center
            gap: 20px
            border-radius: 5px
            background-color: $lightModeElements
            box-shadow: 0 2px 2px $shadowColor
            padding: 0 30px
            box-sizing: border-box

            .search-icon
                width: 20px
                height: 20px

            input
                width: 100%
                height: 50%
                border: none
                color: $lightModeText
                letter-spacing: 1px
                color: $lightModeInput
                font: 
                    size: $homepageFont
                    family: 'Nunito Sans', sans-serif
                

                &:focus
                    border: none
                    outline: none

        .region-select
            width: 200px
            height: 60px
            font: 
                size: $homepageFont
                family: 'Nunito Sans', sans-serif
            border: none
            padding: 0 25px

            &:focus
                outline: none
    
</style>
