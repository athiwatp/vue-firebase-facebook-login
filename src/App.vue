<template>
  <div id="app">
    <img src="./assets/logo.png">
    <button @click="sign()"> signin </button>
    <button @click="signOut()"> signout </button>
    <router-view></router-view>
  </div>
</template>

<script>
import firebase from 'firebase'
var config = {
  apiKey: 'AIzaSyAUW0HgyW7nBGBrUPdlWmDBMpHUHOSwpB0',
  authDomain: 'fir-auth-12e52.firebaseapp.com',
  databaseURL: 'https://fir-auth-12e52.firebaseio.com',
  storageBucket: 'fir-auth-12e52.appspot.com',
  messagingSenderId: '221877419354'
}
firebase.initializeApp(config)
var provider = new firebase.auth.FacebookAuthProvider()
// provider.addScope('public_profile')
provider.addScope('email')
provider.setCustomParameters({
  'display': 'popup'
})
export default {
  name: 'app',
  data () {
    return {
    }
  },
  methods: {
    sign () {
      console.log('yes')
      firebase.auth().signInWithPopup(provider).then(function (result) {
        var token = result.credential.accessToken
        var user = result.user
        console.log(token, user)
      }).catch(function (error) {
        console.log(error)
      })
    },
    signOut () {
      firebase.auth().signOut().then(function () {}, function (error) {
        console.log(error)
      })
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
