<template>
  <GameScreen />
</template>

<script>
import GameScreen from './components/GameScreen.vue'

export default {
  name: 'App',
  components: {
    GameScreen
  }
}
</script>

<style lang="sass">
@font-face 
  font-family: "Qarmic Sans"
  src: url('./assets/fonts/Qarmic sans Abridged.ttf')


#app 
  font-family: "Qarmic Sans"
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  text-align: center
  color: #2c3e50
  box-sizing: border-box
  background: #f4f4f4
  width: 100%
  height: 100%
  padding: 20px
  display: flex

body 
  margin: 0
  height: 100vh
  width: 100vw

</style>
