<template>
    <div id="app">
        <app-title-header></app-title-header>
        <div class="content">
            <div class="name-list-wrapper">
                <div class="name-list">
                    <header>
                        <h2 class="header">Lista imion</h2>
                    </header>
                    <name-input
                            v-if="showNamesInput"
                            @NamesInput-SAVE="saveNames($event)"
                            @NamesInput-CANCEL="showNamesInput = false"
                    ></name-input>
                    <name-to-do-list
                            v-else
                            @NameList-EDIT="showNamesInput = true"
                            :names="names"
                            :namesLeft="namesLeft.length"
                    ></name-to-do-list>
                </div>
            </div>
            <div class="name-chooser-content">
                <welcome-instruction v-if="namesLeft.length === 0"></welcome-instruction>
                <name-disqualifier
                        v-if="namesLeft.length > 1"
                        :names="namesToDecide"
                        @NameDisqualifier-DISQUALIFY_NAMES="disqualifyNames($event)"
                ></name-disqualifier>
                <winner-information
                        v-if="winner"
                        :winner="winner"
                ></winner-information>
            </div>
        </div>
    </div>
</template>

<script>
import NameDisqualifier from './components/NameDisqualifier'
import NameToDoList from './components/NameToDoList'
import NameInput from './components/NamesInput'
import WelcomeInstruction from './components/WelcomeInstruction'
import WinnerInformation from './components/WinnerInformation'
import AppTitleHeader from './components/AppTitleHeader'
import _ from 'lodash'

export default {
  name: 'app',
  components: {
    NameDisqualifier,
    NameToDoList,
    NameInput,
    WelcomeInstruction,
    WinnerInformation,
    AppTitleHeader
  },
  data () {
    return {
      names: [],
      showNamesInput: false
    }
  },
  methods: {
    saveNames: function (names) {
      this.names = names
      this.showNamesInput = false
    },
    disqualifyNames: function (disqualifiedNames) {
      for (let name of disqualifiedNames) {
        name.disqualified = true
      }
    }
  },
  computed: {
    namesToDecide: function () {
      let yetToDecideNames = _.filter(this.names, (name) => {
        return (name.disqualified === false)
      })

      yetToDecideNames = _.shuffle(yetToDecideNames)
      yetToDecideNames.splice(this.namesToDecideCount)
      return yetToDecideNames
    },
    namesLeft: function () {
      return _.filter(this.names, (name) => {
        return (name.disqualified === false)
      })
    },
    winner: function () {
      const notDisqualifiedYet = _.filter(this.names, (name) => {
        return (name.disqualified === false)
      })

      if (notDisqualifiedYet.length === 1) {
        return notDisqualifiedYet[0]
      } else {
        return false
      }
    },
    namesToDecideCount: function () {
      const min = 2
      const max = 5
      const step = 10
      let additional = Math.floor(Math.min(this.namesLeft.length, max * step - min * step) / step)

      return min + additional
    }
  }
}
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

*::before,
*::after {
    box-sizing: inherit;
}

html {
    font-size: 10px;
}

body {
    font-size: 1.6rem;
    background-image: linear-gradient(to top, lightgrey 0%, lightgrey 1%, #e0e0e0 26%, #efefef 48%, #d9d9d9 75%, #bcbcbc 100%);

}

button {
    cursor: pointer;
}

button::-moz-focus-inner {
    border: 0;
}

pre {
    border: 1px solid black;
    background-color: lightgray;
    border-radius: 4px;
    padding: 0.5rem;
    margin: 1rem;
    display: block;
    text-align: left;
}

#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
}

.content {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
    height: 80vh;
}

.name-list-wrapper {
    min-width: 300px;
    width: 20vw;
    height: 100%;
    background-image: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}

.name-chooser-content {
    justify-content: center;
    justify-items: center;
    align-items: center;
    align-content: center;
    display: flex;
    flex-direction: column;
    flex: 1;
    padding: 0 6rem;
    width: 80vw;
}

.name-list {
    border-top: 1px solid darkslategray;
    display: flex;
    flex-direction: column;
}

.name-list .header {
    border-bottom: 1px solid lightslategray;
    text-align: center;
}

</style>
