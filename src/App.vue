<template>
  <div id="app">
    <h1>Brewdog</h1>
    <label for="beer_select">Select a Beer:</label>
    <select id="beer_select" v-model="selectedBeer">
      <option value="" disabled>Select a beer</option>
      <option v-for="beer in beers" :key="beer.id" :value="beer"> {{beer.name}} </option>
    </select>

    <div class="main-container">

      <beer-detail :favouriteBeers="favouriteBeers" :selectedBeer="selectedBeer" :beer="selectedBeer"></beer-detail>
      <favourite-beers :favouriteBeers="favouriteBeers"></favourite-beers>
    </div>
  </div>
</template>

<script>

import BeerDetail from './components/BeerDetail.vue';
import BeersList from './components/BeersList.vue';
import FavouriteListItem from './components/FavouriteListItem.vue';
import ListIngredient from './components/ListIngredient.vue';
import {eventBus} from './main.js';

export default {
  name: 'App',
  data(){
    return {
      beers:[],
      selectedBeer: null,
      favouriteBeers: []
    }
  },
  components: {
    'beer-detail': BeerDetail,
    'favourite-beers': FavouriteListItem,
    'beers-list': BeersList,
    'list-ingredient': ListIngredient
  },
  mounted(){
      fetch('https://api.punkapi.com/v2/beers')
      .then(res => res.json())
      .then(beers => this.beers = beers)
    
    eventBus.$on('beer-selected', (beer) => {
      this.selectedBeer = beer;
    })
    eventBus.$on('fave-beer', (beer) => {
      this.favouriteBeers.push(beer)
    })
    eventBus.$on('remove-beer', (beer) => {
      this.favouriteBeers.splice(this.favouriteBeers.indexOf(beer), 1)
    })
  },
  methods: {
    
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.main-container {
  display: flex;
  justify-content: space-between;
}
.beer-img {
  height: 200px;
}
.small-beer {
  height: 60px;
}

favourite-beers {
  display: flex;
  flex-direction: column;

}

</style>


