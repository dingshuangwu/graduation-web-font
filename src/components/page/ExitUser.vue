<template >
  <div>
  </div>
</template>

<script>
import { clearLocalStorage, removeName, removeToken, removeJurisdiction, removeImageUrl } from '../../utils/auth'
export default {
  name: 'Exit',
  data() {
    return {
      msg: '退出登录'
    }
  },
  methods: {
    exitUser: function() {
      this.$axios.post(
        'api/login/loginOut',
        {},
        response => {
          // eslint-disable-next-line eqeqeq
          if (response.code == '200') {
            removeName()
            removeToken()
            removeImageUrl()
            removeJurisdiction()
            this.$store.commit('SET_NAME', '')
            this.$store.commit('SET_TOKEN', '')
            this.$store.commit('SET_JURISDICTION', {})
            this.$store.commit('SET_IMAGEURL', '')
            clearLocalStorage()
            this.$router.push({ path: '/' })
            console.log(response.message)
          }
          this.$router.push({ path: '/' })
        }
      )
    }
  },
  mounted() {
    setTimeout(this.exitUser(), 10)
  }
}

</script>

  <!--Add "scoped" attribute to limit CSS to this component only -->
<style scoped >
</style>
