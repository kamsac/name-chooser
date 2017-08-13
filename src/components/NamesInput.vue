<template>
    <div class="wrapper">
        <label class="label">Podaj imiona (jedno na linię):</label>
        <textarea class="input" v-model="namesInput"></textarea>
        <div class="buttons">
            <button class="save-button" v-on:click="saveNames()">Ustaw imiona</button>
            <button class="cancel-button" v-on:click="cancel()">Wróć</button>
        </div>
    </div>
</template>

<script>
  export default {
    name: 'names-input',
    data () {
      return {
        names: [],
        namesInput: ''
      }
    },
    methods: {
      clearNames: function () {
        this.names = []
      },
      saveNames: function () {
        this.clearNames()

        const inputArr = this.namesInput.trim().split('\n').filter((el) => {
          return (el !== '')
        })

        this.names = inputArr.map((name) => {
          return {
            name: name,
            disqualified: false
          }
        })

        this.$emit('NamesInput-SAVE', this.names)
      },
      cancel: function () {
        this.$emit('NamesInput-CANCEL')
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

    .label {
        align-self: flex-start;
    }

    .input {
        resize: vertical;
        background-color: Lavender;
        height: 50vh;
        color: black;
    }

    .buttons {
        display: flex;
        flex-direction: row;
    }

    .buttons > * {
        margin-right: 1rem;
    }

    .buttons > *:last-child {
        margin-right: 0;
    }

    .save-button {
        background-color: YellowGreen;
        color: black;
        padding: 1rem;
        border-radius: 4px;
        flex: 2;
    }

    .cancel-button {
        background-color: Crimson;
        color: black;
        padding: 1rem;
        border-radius: 4px;
        flex: 1;
    }
</style>
