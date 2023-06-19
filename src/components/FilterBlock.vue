<script setup></script>

<script>
export default {
  data() {
    return {
      searchQuery: "",
      regionsArray: ["Africa", "Americas", "Asia", "Europe", "Oceania", "All"],
    };
  },
  props: ["filter", "isOpen", "mode", "loading"]
};
</script>

<template>
  <div class="forms-wrapper">
    <form
      @submit.prevent="$emit('setSearchQuery', searchQuery)"
      action=""
      class="search-form"
    >
      <img class="search-icon" src="../assets/search.svg" alt="Search icon" />
      <input
        type="text"
        v-model="searchQuery"
        placeholder="Search for a country..."
      />
    </form>
    <div class="filter-wrapper">
      <div class="current-filter-wrapper" @click="$emit('openMenu')">
        <p>{{ filter }}</p>
        <div class="custom-arrow"></div>
      </div>
      <ul class="region-select" v-show="isOpen">
        <li
          v-for="region in regionsArray"
          key="region"
          @click="$emit('setFilter', region)"
        >
          {{ region }}
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped lang="sass">

@import '../input.sass'

.forms-wrapper
    position: relative
    width: 100%
    display: flex
    justify-content: space-between
    padding: 0 80px
    box-sizing: border-box
    margin-top: 50px

    @media screen and (max-width: 400px) 
      flex-direction: column
      gap: 20px
      padding: 0 20px

    .search-form
        width: 480px
        height: 60px
        display: flex
        align-items: center
        gap: 20px
        border-radius: 5px
        background-color: v-bind('mode.elementColor')
        box-shadow: 0 2px 2px v-bind('mode.shadowColor')
        padding: 0 30px
        box-sizing: border-box

        @media screen and (max-width: 400px) 
          width: 100%

        .search-icon
            width: 20px
            height: 20px

        input
            width: 100%
            height: 50%
            border: none
            letter-spacing: 1px
            color: v-bind('mode.fontColor')
            background-color: inherit
            font:
                size: $homepageFont
                family: 'Nunito Sans', sans-serif

            &::placeholder
                color: v-bind('mode.fontColor')

            &:focus
                border: none
                outline: none

        .loading
            width: 40px

    .filter-wrapper
        width: 200px
        position: relative
        color: v-bind('mode.fontColor')

        @media screen and (max-width: 400px) 
              font-size: $homepageFont

        .current-filter-wrapper
            display: flex
            align-items: center
            justify-content: space-between
            width: 100%
            height: 60px
            padding: 0 25px
            border-radius: 10px
            box-shadow: 0 4px 4px 4px v-bind('mode.shadowColor')
            background-color: v-bind('mode.elementColor')
            box-sizing: border-box

            &:hover
                cursor: pointer

            .custom-arrow
                width: 10px
                height: 10px
                border-top: 2px solid v-bind('mode.fontColor')
                border-left: 2px solid v-bind('mode.fontColor')
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
            box-shadow: 0 4px 4px 4px v-bind('mode.shadowColor')
            background-color: v-bind('mode.elementColor')

            li
                &:hover
                    cursor: pointer
</style>
