<template src="./Login.html"></template>
<script>
import Vue from 'vue'
import axios from 'axios'
Vue.use(axios)

export default {
  name: 'login',
  data () {
    return {
      email: '',
      password: '',
      keepLoggedIn: false,
      emailErrors: [],
      passwordErrors: [],
    }
  },
  computed: {
    formReady () {
      return !this.emailErrors.length && !this.passwordErrors.length
    },
  },
  methods: {
    onsubmit () {
      this.emailErrors = this.email ? [] : ['Email is required']
      this.passwordErrors = this.password ? [] : ['Password is required']
      if (!this.formReady) {
        return
      }
      const loginURL = 'http://devapi.trackervigil.com/jwt/userdblogin.php'
      const params = {
        username: this.email,
        password: this.password,
      }
      axios.post(loginURL, JSON.stringify(params))
        .then((response) => {
          console.log(response)
          if (response.data.Status === 1) {
            localStorage.setItem('tocken', response.data.tocken)
            localStorage.setItem('loginUserName', response.data.username)
            localStorage.setItem('loginflag', true)

            this.$router.push({ name: 'dashboard' })
          } else {
            alert(response.data.Message)
          }
        })
    },
  },
  created () {
    localStorage.loginflag = false
  },
}
</script>
<style lang="scss">
</style>
