<template>
  <q-dialog ref="dialogRef" @hide="onDialogHide">

  <q-card flat bordered class="my-card bg-grey-1">
      <q-card-section>
        <div class="row items-center no-wrap">
          <div class="col">
            <div class="text-h6">Create a Group</div>
            <div class="text-subtitle2"></div>
          </div>

        </div>
      </q-card-section>
         <q-input v-model="name" label="Group Name"/>
         <q-toggle
         v-model="approvable"
         color="green"
         label="Approve Hours"
         left-label
       />

      <q-card-section>
      </q-card-section>

      <q-separator />

      <q-card-actions>
        <q-btn flat>CANCEL</q-btn>
        <q-btn flat @click = "onOkClick">CREATE</q-btn>
      </q-card-actions>
    </q-card>

  </q-dialog>
</template>

<script>
import { defineComponent, ref} from "vue"
import { useDialogPluginComponent } from 'quasar'
import { API } from 'aws-amplify';
import {createGroup} from '../graphql/mutations'
export default defineComponent({
  name: 'CreateDialog',
  emits: [

  ...useDialogPluginComponent.emits
],
  setup() {

       const { dialogRef, onDialogHide, onDialogOK, onDialogCancel } = useDialogPluginComponent()
       const name = ref("")
       const approvable = ref(false)

       const create = async () => {
         const resp = await API.graphql({
           query: createGroup,
           variables: {
             input:{
             name: name.value
           }}
         })

         console.log(resp)
       }

       return {
         approvable,
         name,
         dialogRef,
         onDialogHide,


        async onOkClick () {
          await create()
           onDialogOK()

         },

         onCancelClick: onDialogCancel
       }
     }
})
</script>

<style lang="css" scoped>
</style>
