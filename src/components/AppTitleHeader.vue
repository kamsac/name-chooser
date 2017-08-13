<template>
    <header class="app-title-header">
        <!--<img src="../assets/logo.png">-->
        <h1 class="title">Wybierator Imienia</h1>
    </header>
</template>

<script>
  export default {
    name: 'app-title-header'
  }
</script>

<style scoped>
    .app-title-header {
        background-image: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        text-align: center;
        display: flex;
        flex-direction: column;
        height: 20vh;
        justify-content: center;
        align-items: center;
    }

    .title {
        padding: 0 2rem;
        border-bottom: 4px solid rosybrown;
        color: whitesmoke;
        font-size: 6vh;
    }
</style>
