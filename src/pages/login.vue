<template>
  <q-page padding class = "column justify-center items-center" style = "width: 100%">
    <transition name = "signInAnim" mode = "out-in">
    <register
    v-if = "signingUp"
    />
    <signin
    v-else
    @signedin = "gotohome"
    />
  </transition>
  <q-btn flat
    label = "toggle"
    @click = "toggle"
  />
  </q-page>
</template>

<script>
import signin from "src/components/signin.vue"
import register from "src/components/register.vue"
import { defineComponent, ref, watch } from 'vue';
import { onAuthUIStateChange } from '@aws-amplify/ui-components'
import { useRouter } from 'vue-router'
import { API } from 'aws-amplify';

export default defineComponent( {
  components: {
    signin,
    register
  },
  setup(){

    const signingUp = ref(false)
    const toggle = () => {
      signingUp.value = !signingUp.value
    }
    const router = useRouter()
    const gotohome = () => {
      router.push("/home")
    }


    return{
      signingUp,
      toggle,
      gotohome
    }
  }
})
</script>

<style>
.signInAnim-enter-active,.signInAnim-leave-active{
  transition: opacity 500ms;
}
.signInAnim-enter-from,.signInAnim-leave-to{
  opacity:0;
}

</style>
