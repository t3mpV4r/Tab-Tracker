<template lang="pug">
  v-layout(row text-xs-center)
    v-flex(xs6 offset-xs3)
      panel(title="Login")
        v-text-field(label="Email" v-model="email")
        v-text-field(label="Password" type="password" v-model="password")
        .error(v-html="error")
        v-btn.cyan(@click="login" dark) Login
</template>

<script>
import AuthenticationService from '@/services/AuthenticationService'
import Panel from '@/components/Panel'

export default {
  data () {
    return {
      email: '',
      password: '',
      error: null
    }
  },
  methods: {
    async login () {
      try {
        const response = await AuthenticationService.login({
          email: this.email,
          password: this.password
        })
        this.$store.dispatch('setToken', response.data.token)
        this.$store.dispatch('setUser', response.data.user)
      } catch (error) {
        this.error = error.response.data.error
      }
    }
  },
  components: {
    Panel
  }
}
</script>
<style  scoped>
.error {
  color:red;
}
</style>
