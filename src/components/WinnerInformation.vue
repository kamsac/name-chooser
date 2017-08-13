<template>
    <div class="winner-information">
        <h2 class="header">Mamy zwycięzcę!</h2>
        <strong class="winner">{{ winner.name }}</strong>
    </div>
</template>

<script>
  export default {
    name: 'winner-information',
    props: ['winner']
  }
</script>

<style scoped>

    @keyframes shadow {
        from {
            text-shadow: 0 0 DeepPink;
        }

        to {
            text-shadow: 0.5rem 0.5rem DeepPink;
        }
    }

    @keyframes rotate {
        from {
            transform: rotate(-4deg);
        }

        to {
            transform: rotate(4deg);
        }
    }

    .winner-information {
        display: flex;
        flex-direction: column;
        text-align: center;
    }

    .header {
        font-size: 8vh;
    }

    .winner {
        margin: 2rem;
        font-size: 12vh;

        animation-name: rotate, shadow;
        animation-duration: 3s, 1.5s;
        animation-timing-function: ease-in-out, ease-in;
        animation-iteration-count: infinite;
        animation-direction: alternate;
    }
</style>
