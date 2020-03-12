<template lang="pug">
  section.countries
      .container-box
        label Pays
        input(v-model="search" @click="onChange" placeholder="Saisissez votre pays" label="Pays")
        //- p Votre pays est : {{search}}

        ul.container-box-content(v-if="showModal")
          li(v-for="item in countries" :key="item.name").container-box-content__list
            img.container-box-content__img(:src="item.flag" alt="flag of this countrie")
            span.container-box-content__name {{ item.name }}

      div(style="margin-top: 50px")
        span {{`Votre pays choisi est: ${this.search}`}}


</template>

<script>
import Autocomplete from './components/Autocomplete';
import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'

Vue.use(VueAxios, axios)


export default {
  name: 'App',

  components: {
    Autocomplete,
  },

  data() {
    return {
      countries: [],
      search: '',
      showModal: false,
      items: [
        {
          id: 0,
          countrie: "Allemagne"
        },
        {
          id: 1,
          countrie: "Brésil"
        },
        {
          id: 2,
          countrie: "Croatie"
        },
        {
          id: 3,
          countrie: "Danemark"
        },
        {
          id: 4,
          countrie: "Espagne"
        },
        {
          id: 5,
          countrie: "France"
        },
        {
          id: 6,
          countrie: "Germany"
        },
      ]
    }
  },

  methods: {
    // 
    onChange() {
      // 
      this.showModal = true 
      console.log('Votre texte est:', this.search)
    } 
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




};
</script>

<style lang="scss">
.countries {
  background:  #f2f5f7;
  height: 100vh;
  display: flex;
  justify-content: center;
  & .container-box {
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
    }
    &-content {
      background-color: #fff;
      border-radius: 3px;
      height: 130px;
      position: absolute;
      top: 70px;
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
}
  
</style>


