<template>
<q-card style="width: 300px; max-width: 100%" >
  <q-card-section class="text-white">
    <q-input
      v-model="code"
      label="Confirmation Code"
    />
  </q-card-section>
<q-card-actions align="right">
    <q-btn flat
      label = "Confirm"
      @click = "confirm"
    />
</q-card-actions>
</q-card>
</template>

<script>
import { defineComponent, ref } from 'vue';
import {Auth} from "aws-amplify";
export default defineComponent( {
  emits: ["confirmed"],
  props: {
    username: {
      type: String,
      required: true
    }
  },
  setup(props, {emit}){
    const code = ref(0)

    const confirm = async() => {
      try {
        await Auth.confirmSignUp(props.username, code.value)
        emit("confirmed")
      } catch(e){
        console.log(e)
      }
    }


    return{
      confirm,
      code
    }
  }
})

</script>

<style lang="css" scoped>
</style>
