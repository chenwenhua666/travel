<template>
 <div>
   <city-headers></city-headers>
   <city-search :cities="cities"></city-search>
   <city-list :hotCities="hotCities" :cities="cities" :letter="letter"></city-list>
   <city-alphabet :cities="cities" @change="getClickedLetter"></city-alphabet>
 </div>
</template>

<script>
import CityHeaders from './components/Header'
import CitySearch from './components/Search'
import CityList from './components/List'
import CityAlphabet from './components/Alphabet'
import axios from 'axios'
export default {
  name: 'City',
  components: {
    CityHeaders,
    CitySearch,
    CityList,
    CityAlphabet
  },
  data () {
    return {
      hotCities: [],
      cities: {},
      letter: ''
    }
  },
  methods: {
    getAllCitiesInfo () {
      axios.get('/api/city.json').then(this.resultSucc)
    },
    resultSucc (res) {
      if (res.data.ret && res.data.data) {
        this.hotCities = res.data.data.hotCities
        this.cities = res.data.data.cities
      }
    },
    getClickedLetter (val) {
      this.letter = val
    }
  },
  mounted () {
    this.getAllCitiesInfo()
  }
}
</script>

<style>
</style>
