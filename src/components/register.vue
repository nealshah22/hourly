<template>
  <transition name = "singUpAnim" mode = "out-in">
  <signup
  v-if = "signingUp"
  @username = "confirmUser"
  />
  <confSignUp
  v-else
  @confirmed = "confirmedUser"
  :username = "username"
  />
  </transition>
</template>

<script>
import { useRouter } from 'vue-router'
import confSignUp from "src/components/confSignUp.vue"
import signup from "src/components/signup.vue"
import { defineComponent, ref } from 'vue';
import {Auth, API} from "aws-amplify";
export default defineComponent( {
  components: {
    confSignUp,
    signup
  },
  setup(){
    const router = useRouter()
    const signingUp = ref(true)
    const username = ref("")
    const confirmUser = (user) => {
      signingUp.value = !signingUp.value
      username.value = user
    }
    const confirmedUser = async () => {
      console.log(await Auth.currentAuthenticatedUser({
        bypassCache: true
      }))
      router.push("/home")
    }

    return{
      confirmedUser,
      confirmUser,
      signingUp,
      username
    }
  }
})

</script>

<style lang="css" scoped>
.signUpAnim-enter-active,.signUpAnim-leave-active{
  transition: opacity 500ms;
}
.signUpAnim-enter-from,.signUpAnim-leave-to{
  opacity:0;
}



</style>
