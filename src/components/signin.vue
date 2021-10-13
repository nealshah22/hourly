<template>
  <q-card style="width: 300px; max-width: 100%" >
    <q-card-section class="text-white">
<!-- add header section -->
      <q-input
        v-model="email"
        label="Your email *"
          />

      <q-input
        v-model="password"
        label="Your password *"
      />

    </q-card-section>
  <q-card-actions align="right">
      <q-btn flat
        label = "sign in"
        @click = "signin"
      />
  </q-card-actions>
  </q-card>
</template>

<script>
import { defineComponent, ref } from 'vue';
import {Auth} from "aws-amplify";
export default defineComponent( {
emits : ["signedin"],
  setup(props, {emit}){
    // const router = useRouter()
    const email = ref("")
    const password = ref("")
    const signin = async() => {
      try {
        const user = await Auth.signIn(email.value, password.value)
        emit("signedin")
      } catch(e){
        console.log(e)
      }
    }


    return{
      email,
      password,
      signin
    }
  }
})

</script>

<style lang="css" scoped>
</style>
