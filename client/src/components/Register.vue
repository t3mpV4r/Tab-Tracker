<template lang="pug">
  v-layout(row text-xs-center)
    v-flex(xs6 offset-xs3)
      panel(title="Register")
        form(name="tab-tracker-form" autocomplete="off")
        v-text-field(label="Email" v-model="email")
        v-text-field(label="Password" type="password" v-model="password")
        div
          font(color="red" v-html="error") asd
        v-btn.cyan(@click="register" dark) Register
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
    async register () {
      try {
        const response = await AuthenticationService.register({
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
