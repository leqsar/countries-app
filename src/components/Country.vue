<script setup></script>

<script>
export default {
  props: ["country", "countries"],
  methods: {
    nativeName() {
      const nativeLang = Object.keys(this.country.languages)[0];
      return this.country.name.nativeName[nativeLang].common;
    },
    currency() {
      const currencyCode = Object.keys(this.country.currencies)[0];
      const currency = this.country.currencies[currencyCode].name;
      const currencySplited = currency.split("");
      currencySplited[0].toUpperCase();
      return currencySplited.join("");
    },
    langs() {
      const langsArray = [];
      for (const lang in this.country.languages) {
        langsArray.push(this.country.languages[lang]);
      }
      return langsArray.join(", ");
    },
    borderCountries() {
      const codedBorderCountries = this.country.borders;
      const borderCountries = [];
      codedBorderCountries.forEach((countryCode) => {
        const decodedName = this.countries.filter((country) => {
          return country.cca3 === countryCode;
        })[0].name.common;
        borderCountries.push(decodedName);
      });
      return borderCountries;
    },
  },
};
</script>

<template>
  <div class="details-page">
    <button class="return-button" @click="$emit('showHome')">
      <img src="../assets/arrow.svg" />
      Back
    </button>
    <div class="details-wrapper">
      <img
        class="details-img"
        :src="country.flags.svg"
        :alt="country.flags.alt"
      />
      <div class="details-info-wrapper">
        <h2>{{ country.name.common }}</h2>
        <ul class="details-info">
          <li><b>Native Name:</b> {{ nativeName() }}</li>
          <li><b>Population:</b> {{ country.population }}</li>
          <li><b>Region:</b> {{ country.region }}</li>
          <li><b>Sub Region:</b> {{ country.subregion }}</li>
          <li><b>Capital:</b> {{ country.capital[0] }}</li>
          <li><b>Top Level Domain:</b> {{ country.tld[0] }}</li>
          <li><b>Currencies:</b> {{ currency() }}</li>
          <li><b>Languages:</b> {{ langs() }}</li>
        </ul>
        <div class="border-details">
          <p><b>Border Countries:</b></p>
          <ul>
            <li v-for="country in borderCountries()" @click="$emit('showBorderDetails', country)">{{ country }}</li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="sass">

@import '../input.sass'

.details-page
    width: 100%
    padding: 0 80px
    margin-top: 80px

    .return-button
        display: flex
        align-items: center
        gap: 10px
        width: 140px
        height: 40px
        padding: 0 30px
        background-color: $lightModeElements
        border: none
        font-size: $detailsFont
        box-shadow: 0 2px 2px 2px $shadowColor

        &:hover
            cursor: pointer

        img
            width: 15px
            height: 15px

    .details-wrapper
        display: flex
        gap: 125px
        width: 100%
        margin-top: 80px

        .details-img
            width: 560px

        .details-info-wrapper
            width: 600px
            display: flex
            flex-direction: column
            padding-top: 60px

            .details-info
                display: flex
                flex-direction: column
                flex-wrap: wrap
                gap: 10px
                height: 160px
                margin-top: 40px

                li
                    font:
                        size: $detailsFont
                        weight: 600

            .border-details
                display: flex
                margin-top: 80px

                ul
                    display: flex
                    width: 450px
                    flex-wrap: wrap
                    margin-left: 20px
                    gap: 10px

                    li
                        display: flex
                        align-items: center
                        width: auto
                        height: 30px
                        padding: 0 30px
                        background-color: $lightModeElements
                        box-sizing: border-box
                        box-shadow: 0 3px 3px 3px $shadowColor

                        &:hover
                            cursor: pointer
</style>
