<template lang="pug">
.container-box
  label Pays
  input(v-model="search" @click="onChange"  @keyup.up="onChangeKeyUp" @keyup.down="onChangeKeyDown" placeholder="Saisissez votre pays" label="Pays")

  ul.container-box-content(v-if="showModal")
    li(v-for="item in countries" :key="item.name" @click="addCountrie(item.name)").container-box-content__list
      img.container-box-content__img(:src="item.flag" alt="flag of this countrie")
      span.container-box-content__name {{ item.name }}
</template>

<script>
import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'

Vue.use(VueAxios, axios)

  export default {
    name: 'Autocomplete',

  data: () => ({
    // Initialized datas
      countries: [],
      countriesName: [],
      search: '',
      isLoading: false,
      showModal: false,
      counter: 0,
  }),

  methods: {
    onChange() {
      this.$emit("input", this.search);
      this.showModal = true
      // console.log('Votre texte est:', this.search)
      console.log('Votre element est:', this.filterResults())
      // console.log('keydown clicked', this.onChangeKeyDown())
      // console.log('data', this.countries)
    },
    filterResults() {
      // 
      this.countries.map(item => {
        this.countriesName = item.name
        console.log(this.countriesName)
      })
      },

    addCountrie(item) {
      this.search = item,
      this.showModal = false
      console.log(this.search)
    },

    onChangeKeyDown() {
      if(this.counter < this.countries.length) {
        this.counter = this.counter + 1
      }
    },

    onChangeKeyUp() {
      console.log('keyup clicked', this.counter)
    },
  },

  mounted() {
    // Here, i get the api to the mounted of project for display result the countries
      Vue.axios.get('https://restcountries.eu/rest/v2/all')
        .then((res) => {
        // Here, i will be push and assign the response result countries in the data array initialized to top
        this.countries = res.data;
        // console.log(res.data)
      })
      .catch((error) => {
        console.log(error)
      })
  },
}
</script>

<style lang="scss">
.container-box {
  width: 300px;
  padding: 25px;
  background: #fff;
  border-radius: 3px;
  position: relative;
  height: 150px;
  margin-top: 50px;
  input {
    outline: none;
    font-size: 1rem;
    border-bottom: 2px solid;
    border-color: #94bbdc;
    width: 100%;
    font-family: "Campton-BoldDEMO";
    position: relative;
    margin-top: 10px;
  }
  &-content {
    background-color: #fff;
    border-radius: 3px;
    height: 130px;
    position: absolute;
    margin: 0 25px;
    left: 0;
    right: 0;
    overflow: hidden;
    overflow-y: scroll;
    box-shadow: 0 0 8px 0px #94bbdc;
    &__list {
      display: flex;
      align-content: center;
      text-decoration-style: none;
      padding: 15px;
      &:hover {
        background-color: #94badc28;
        cursor: pointer;
      }
    }
    &__img {
      width: 25px;
    }
    &__name {
      margin-left: 15px;
    }
  }
}
</style>
