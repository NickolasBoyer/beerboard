<template lang="pug">
  #app.noselect
    modal
    router-view
</template>

<script>
import modal from './components/modal'
import store from './vuex/store'
import {firebaseApp} from './firebase'

export default {
  store,
  name: 'app',
  components: {
    modal
  },
  created: function () {
    var that = this
    firebaseApp.database().ref(".info/connected")
    .on("value", function (snapshot) {
      that.$store.commit('setServerConnectionState', {newState: snapshot.val()})
    })
  }
}
</script>

<style>
html {
  height: 100%;
  width: 100%;
  background-color: #F6F6F6;
}
body {
  height: 100%;
  width: 100%;
  margin: 0px;
}
#app {
  height: 100%;
  width: 100%;
  font-family: 'Roboto', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.noselect {
  -webkit-touch-callout: none; /* iOS Safari */
    -webkit-user-select: none; /* Safari */
     -khtml-user-select: none; /* Konqueror HTML */
       -moz-user-select: none; /* Firefox */
        -ms-user-select: none; /* Internet Explorer/Edge */
            user-select: none; /* Non-prefixed version, currently
                                  supported by Chrome and Opera */
}
</style>
