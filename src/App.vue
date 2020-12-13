<template>
  <div id="app">

    <SearchBar 
      @search="setSearchRequest"
      v-if="companies_data.length !== 0"
    />

    <ListOfCompanies 
      :companies="data_to_display"
      v-if="companies_data.length !== 0"
    />

    <img 
      src="./assets/loading.gif" 
      alt=""
      class="mx-loading-image"
      v-if="loading"
    />

  </div>
</template>

<script>

const axios = require('axios')

import ListOfCompanies from './components/ListOfCompanies'
import SearchBar from './components/SearchBar'

export default {
  name: 'App',
  components: {
    ListOfCompanies,
    SearchBar
  },
  data() {

    return {

      store_path: 'https://pkgstore.datahub.io/core/s-and-p-500-companies-financials/3/datapackage.json',

      store_name: 'constituents-financials_json',

      sNp500Data: null,

      sNp500Path: null,

      companies_data: [],

      store_type: 'constituents-financials_json',

      data_to_display: [],

      loading: true

    }

  },

  methods: {

    setSearchRequest( str ) {

      let _this = this

      this.data_to_display = []

      this.loading = true

      this.companies_data.forEach( function( element ) {

        let search = str.toLowerCase()

        let name = element.Name.toLowerCase()

        if( name.indexOf( search ) !== -1 ) {

          _this.data_to_display.push( element )

        }

      } )

      setTimeout( function() {

        _this.loading = false

      }, 500 )

    },

    getDada() {

      let _this = this

      axios
      .get( _this.store_path )
      .then( function( res ) {

        _this.sNp500Data = res.data.resources

      } )

    }

  },

  watch: {

    companies_data() {

      if( this.companies_data ) {

        this.data_to_display = this.companies_data

      }

    },

    sNp500Data() {

      let _this = this

      if( this.sNp500Data ) {

        this.sNp500Data.forEach( function( element ) {

          if( element.name === _this.store_type ) {

            _this.sNp500Path = element.path

          }
          
        } )

      }

    },

    // now lets watch the sNp500Path model
    sNp500Path() {

      let _this = this

      if( this.sNp500Path ) {

        axios
        .get( _this.sNp500Path )
        .then( function( res ) {

          // get the data of s&p500 companies
          _this.companies_data = res.data

          _this.loading = false

        } )

      }

    }

  },

  mounted() {

    this.getDada()

  }

}
</script>

<style>
  .mx-loading-image {
    width: 50px;
    margin: 50px auto;
    display: block;
  }
  @import url(./assets/bootstrap.min.css);
</style>
