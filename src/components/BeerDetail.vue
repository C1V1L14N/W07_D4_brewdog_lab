<template>
    <div v-if="beer" id="selected-beer">
        <h2>Beer: {{beer.name}}</h2>
        <p id="tagline">{{beer.tagline}}</p>
        <p>Born on: {{beer.first_brewed}}</p>
        <p id="beer-descrption">Description: {{beer.description}}</p>
        <p>________________________</p>
        <h3>Ingredients:</h3>
        <p>{{beer.ingredients.malt[0].name}}</p>
        <ul>
            <list-ingredients v-for="(ingredient, index) in ingredients" :ingredient="ingredient" :key="index"></list-ingredients>
        </ul>
        <img class="beer-img" :src="beer.image_url" alt="beer.name"/>

        <button v-if="!favouriteBeers.includes(selectedBeer)" v-on:click="addToFavourites">Save to Favourites</button>
        <button v-if="favouriteBeers.includes(selectedBeer)" v-on:click="removeFromFavourites">Remove from Favourites?</button>
    </div>
    <div v-else>
        <p>Go on! Pick a Beer!</p>
    </div>


</template>

<script>
import {eventBus} from '../main.js'
import ListIngredient from './ListIngredient.vue';

export default {
    name: 'beer-detail', 
    props: ['beer', 'favouriteBeers', 'selectedBeer'],
    methods: {
        addToFavourites: function(){
            eventBus.$emit('fave-beer', this.beer)
    },
        removeFromFavourites: function() {
            eventBus.$emit('remove-beer', this.beer)
        }
    }
}
</script>

<style>

#tagline {
    font-style: italic;
}



</style>