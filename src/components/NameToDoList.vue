<template>
    <div class="wrapper">
        <p class="progress">Pozostało imion: {{ namesLeft }}</p>
        <ul class="name-paper-list">
            <li class="item" v-for="name in names">
                <span v-bind:class="{disqualified: name.disqualified}">{{ name.name }}</span>
            </li>
        </ul>
        <button class="edit-button" @click="editNames">Edytuj imiona</button>
    </div>
</template>

<script>
  export default {
    name: 'name-to-do-list',
    props: [
      'names',
      'namesLeft'
    ],
    methods: {
      editNames: function () {
        this.$emit('NameList-EDIT', true)
      }
    }
  }
</script>

<style scoped>
    .wrapper {
        display: flex;
        flex-direction: column;
    }

    .wrapper > * {
        margin: 1rem 1rem 0 1rem;
    }

    .wrapper > *:last-child {
        margin-bottom: 1rem;
    }

    .name-paper-list {
        text-align: left;
        padding: 2rem 2rem;
        list-style-type: disc;
        background-color: FloralWhite;
        list-style-position: inside;
        border: 1px solid black;
        overflow-y: auto;
        height: 50vh;
    }

    .item {
        border-bottom: 1px solid cornflowerblue;
        padding-left: 1rem;
        text-overflow: ellipsis;
        overflow: hidden;
    }

    .disqualified {
        transition: all 1s;
        color: RosyBrown;
        text-decoration: line-through;
        text-decoration-color: Crimson;
        text-decoration-style: double;
    }

    .edit-button {
        background-color: lightgray;
        color: black;
        padding: 1rem;
        border-radius: 4px;
    }
</style>
