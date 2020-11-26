<template lang="html">
    <div>
        <ul>
            <list-item v-for="(beer, id) in beers" :beer="beer" :key="id"></list-item>
        </ul>
    </div>
</template>

<script>
import ListItem from './ListItem.vue';

export default {
    name: 'beers-list',
    props: ['beers'],
    components: {
        "list-item": ListItem
    }
}
</script>

<style>

</style>