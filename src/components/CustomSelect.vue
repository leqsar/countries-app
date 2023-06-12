<script setup>

</script>

<script>
    export default {
        data() {
            return {
                filter: 'Filter by Region',
                regionsArray: ['Africa', 'America', 'Asia', 'Europe', 'Oceania', 'All' ],
                isOpen: false
            }
        },
        methods: {
            setFilter(event) {
                this.filter = event.currentTarget.textContent
                this.isOpen = false
            },
            openMenu() {
                this.isOpen = !this.isOpen
            }
        }
    }

</script>

<template>
    <div class="filter-wrapper">
        <div class="current-filter-wrapper" @click="openMenu">
            <p>{{ filter }}</p>
            <div class="custom-arrow"></div>
        </div>
        <ul class="region-select" v-show="isOpen">
            <li v-for="region in regionsArray" key="region" @click="setFilter">
                {{ region }}
            </li>
        </ul>
    </div>
</template>

<style scoped lang="sass">

    @import '../input.sass'

    .filter-wrapper
        width: 200px
        position: relative

        .current-filter-wrapper
            display: flex
            align-items: center
            justify-content: space-between
            width: 100%
            height: 60px
            padding: 0 25px
            border-radius: 10px
            box-shadow: 0 4px 4px 4px $shadowColor
            box-sizing: border-box

            &:hover
                cursor: pointer

            .custom-arrow
                width: 10px
                height: 10px
                border-top: 2px solid black 
                border-left: 2px solid black 
                transform: rotate(225deg)

        .region-select
            position: absolute
            display: flex
            flex-direction: column
            justify-content: space-between
            width: 100%
            height: 200px
            padding: 20px 25px
            box-sizing: border-box
            border-radius: 10px
            box-shadow: 0 4px 4px 4px $shadowColor
            background-color: $lightModeElements

            li
                &:hover
                    cursor: pointer

    
</style>
