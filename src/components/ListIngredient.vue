<template>
    <div>
        <li>{{beer.ingredient.name}}</li>
    </div>
</template>

<script>
import { eventBus } from '../main.js'

export default {
    name: 'list-ingredient',
    props: ['ingredient']
}
</script>

<style>

</style>