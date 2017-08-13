<template>
    <div class="disqualifier">
        <h2 class="question">Które lepsze?</h2>
        <transition name="fade" mode="out-in" >
            <div class="buttons" v-show="showButtons">
                <button
                        v-for="(name, index) in names"
                        :disabled="showButtons === false"
                        :class="getChosenButtonClass(index)"
                        class="button"
                        @click="chooseName($event, index)"
                >{{ name.name }}</button>
            </div>
        </transition>
    </div>
</template>

<script>
  export default {
    name: 'name-disqualifier',
    props: ['names'],
    data () {
      return {
        showButtons: true,
        chosenButtonIndex: -1
      }
    },
    methods: {
      chooseName: function ($event, index) {
        this.showButtons = false
        this.chosenButtonIndex = index

        window.setTimeout(() => {
          let disqualifiedNames = this.names
          disqualifiedNames.splice(index, 1)

          this.$emit('NameDisqualifier-DISQUALIFY_NAMES', disqualifiedNames)
          this.showButtons = true
          this.chosenButtonIndex = -1
        }, 1000)
      },
      getChosenButtonClass (index) {
        if (this.chosenButtonIndex === -1) {
          return ''
        }

        if (index === this.chosenButtonIndex) {
          return 'yes'
        } else {
          return 'nope'
        }
      }
    }
  }
</script>

<style scoped>
    .disqualifier {
        justify-content: center;
        justify-items: center;
        align-items: center;
        align-content: center;
        display: flex;
        flex-direction: column;
        flex: 1;
        width: 100%;
    }

    .question {
        font-size: 5vw;
        margin-bottom: 4vh;
    }

    .buttons {
        padding: 1rem;
        flex: 1;
        justify-content: center;
        display: flex;
        flex-direction: row;
        width: 100%;
    }

    .buttons > * {
        margin-right: 1rem;
    }

    .buttons > *:last-child {
        margin-right: 0;
    }

    .button {
        padding: 5vh 2vh;
        background-color: SlateBlue;
        border: none;
        border-radius: 6px;
        color: white;
        font-size: 3rem;
        flex: 1;
        transition: all 0.1s;
    }

    .button:hover {
        background-color: DarkSlateBlue;
    }

    .yes {
        background-color: LimeGreen !important;
        color: black !important;
    }

    .nope {
        background-color: Crimson !important;
        color: black !important;
    }

    @keyframes fly-away {
        from {
            transform: translateY(0rem);
            opacity: 1;
        }

        to {
            transform: translateY(-3rem);
            opacity: 0;
        }
    }

    @keyframes appear {
        from {
            opacity: 0;
            transform: translateY(-2rem);
        }

        to {
            opacity: 1;
            transform: translateY(0);
        }
    }

    .fade-enter-active, .fade-leave-active, .v-enter-to {
        transition: color 0.5s;
        animation-name: appear;
        animation-duration: 0.5s;
        animation-timing-function: ease;
        animation-iteration-count: 1;
    }

    .fade-enter, .fade-leave-to, .v-leave-to {
        transition: color 1s;
        animation-name: fly-away;
        animation-duration: 1s;
        animation-timing-function: ease;
        animation-iteration-count: 1;
    }
</style>
