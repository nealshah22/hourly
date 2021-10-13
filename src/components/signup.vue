<template>
<q-card style="width: 300px; max-width: 100%" >
  <q-card-section class="text-white">
    <q-input
      v-model="name"
      label="Your name "
    />

    <q-input
      v-model="email"
      label="Your email "
        />

    <q-input
      v-model="phone_number"
      label="Your phone number "
        />

    <q-input
      v-model="password"
      label="Your password "
      type = "password"

    />

    <q-input
      v-model="confirmPassword"
      label="Please confirm password "
      type = "password"
    />

    <q-input
      v-model="grade"
      label="Your grade"
      type = "number"
    />
  </q-card-section>
<q-card-actions align="right">
    <q-btn flat
      label = "sign up"
      @click = "signup"
    />
</q-card-actions>
</q-card>
</template>

<script>
import { defineComponent, ref } from 'vue';
import {Auth, API} from "aws-amplify";
export default defineComponent( {
  emits: ["username"],

  setup(props, {emit}){

    const name = ref("")
    const email = ref("")
    const phone_number = ref("")
    const password = ref("")
    const confirmPassword = ref("")
    const grade = ref(0)

    const signup = async() => {
      const {user} = await Auth.signUp({
        username: email.value,
        password: password.value,
        attributes: {
          phone_number : phone_number.value,
          email: email.value,
          name: name.value
        }
      })
      emit("username", email.value)
    //   // console.log(await Auth.currentSession())
    //   const resp = await API.graphql({
    //     query:`
    //     mutation CreateUser(
    //       $input: CreateUserInput!
    //       $condition: ModelUserConditionInput
    //     ) {
    //       createUser(input: $input, condition: $condition) {
    //         id
    //         fullname
    //         grade
    //
    //         createdAt
    //         updatedAt
    //       }
    //     }
    //     `,
    //     variables: {
    //       input: {
    //         email: email.value,
    //         fullname: name.value,
    //         grade: grade.value
    //       }
    //     }
    //   })
    }


    return{
      name,
      email,
      phone_number,
      password,
      confirmPassword,
      grade,
      signup
    }
  }
})

</script>

<style lang="css" scoped>
</style>
