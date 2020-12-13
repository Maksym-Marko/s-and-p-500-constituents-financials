<template>
  <div class="search-bar">
    <form>

      <div class="form-group">
        <label for="search_bar">Search By Company Name</label>
        <input
          type="text"
          id="search_bar"
          v-model="search_bar"
          class="form-control" 
        />
      </div>
      
    </form>
   
  </div>
</template>

<script>
export default {

  name: 'SearchBar',

  data() {
    return {

      search_bar: null,

      set_timeout: null

    }
  },

  watch: {

    search_bar() {

      let _this = this

      clearTimeout( this.set_timeout )

      this.set_timeout = setTimeout( function() {

        _this.$emit( 'search', _this.search_bar )

      }, 1000 )

    }

  }

}
</script>

<style scoped>

</style>
