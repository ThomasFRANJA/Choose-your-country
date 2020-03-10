<template lang="pug">
  v-autocomplete(
    label="Pays"
    :color="color"
    :placeholder="placeholder"
    v-model="select"
    :loading="loading"
    :items="items"
    :search-input.sync="search"
    cache-items
    class="mx-4"
    flat
    hide-no-data
    hide-details
    solo-inverted
  )
</template>

<script>
  export default {
    name: 'Autocomplete',

  data: () => ({
    // Initialized datas items states
      loading: false,
      items: [],
      search: null,
      select: null,
      states: [
        'Alabama',
        'Alaska',
        'American Samoa',
        'Arizona',
        'Arkansas',
        'California',
        'Colorado',
        'Connecticut',
        'Delaware',
        'District of Columbia',
      ],
  }),

  watch: {
    search (val) {
      val && val !== this.select && this.querySelections(val)
    }
  },
    
  methods: {
    querySelections (v) {
      this.loading = true
      // Simulated ajax query
      setTimeout(() => {
        this.items = this.states.filter(e => {
          return (e || '').toLowerCase().indexOf((v || '').toLowerCase()) > -1
        })
        this.loading = false
      }, 500)
    },
  },

    props: {
      color: {
        type: String,
        default: "#94bbdc"
      },
      placeholder: {
        type: String,
        default: "Entrez le nom de votre pays"
      },
    }
  }
</script>
