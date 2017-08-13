<template>
    <li
            v-bind:class="{'nope': name.nope}"
    >
        {{ name.name }}
    </li>
</template>

<script>
  export default {
    name: 'name-list-item',
    props: ['name']
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .nope {
        color: crimson;
        text-decoration: line-through;
    }
</style>
