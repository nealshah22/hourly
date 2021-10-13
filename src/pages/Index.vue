<template>
  <q-page class = "q-pa-md">
    <amplify-authenticator>
     <amplify-sign-out>
     </amplify-sign-out>
<div class="q-py-sm">


    <!-- Example Group Card Member-->
       <q-card flat  class="my-card bg-ctmGrey">

             <q-card-section>
               <div class="row items-center no-wrap">
                 <div class="col">
                   <div class="text-h6 text-weight-bolder text-ctmSage" style="font-size: 20pt">
                     Example Group
                   </div>
                   <div class="text-subtitle2 text-ctmSage">Member</div>
                 </div>

                 <div class = "col-5">

                     <div class="text-h4 text-weight-bold text-center text-ctmSage"  style="font-size: 40pt">
                       12
                     </div>
                     <div class="text-subtitle2 text-center text-ctmSage">
                       hours
                     </div>

                  </div>
                  <!-- center "hours" below "12" -->


                 <div class="col-auto">
                   <q-btn color="ctmSage" round flat icon="more_vert">
                     <q-menu cover auto-close>
                       <q-list>
                         <q-item clickable>
                           <q-item-section>Leave Group</q-item-section>
                         </q-item>
                         <q-item clickable>
                           <q-item-section>Share Join Code</q-item-section>
                         </q-item>
                       </q-list>
                     </q-menu>
                   </q-btn>
                 </div>
               </div>
             </q-card-section>

             <q-card-section>

             </q-card-section>

             <q-separator />

             <q-card-actions>
               <q-btn flat color = "ctmSage">Submit Hours</q-btn>
               <q-btn flat></q-btn>
             </q-card-actions>
           </q-card>
</div>
<div class="q-py-sm">


    <!-- Example Group Card Owner-->
       <q-card flat  class="my-card bg-ctmGrey ">
             <q-card-section>
               <div class="row items-center no-wrap">
                 <div class="col">
                   <div class="text-h6 text-weight-bolder text-ctmSage" style="font-size: 20pt">
                     Example Group
                   </div>
                   <div class="text-subtitle2 text-ctmSage">Owner</div>
                 </div>
                 <div class = "col-5">
                   <div class="text-h4 text-weight-bold text-center text-ctmSage"  style="font-size: 40pt">
                     32
                   </div>
                   <div class="text-subtitle2 text-center text-ctmSage">
                     hours
                   </div>
                  </div>

                 <div class="col-auto">
                   <q-btn color="ctmSage" round flat icon="more_vert">
                     <q-menu cover auto-close>
                       <q-list>
                         <q-item clickable>
                           <q-item-section>Delete Group</q-item-section>
                         </q-item>
                         <q-item clickable>
                           <q-item-section>Share Join Code</q-item-section>
                         </q-item>
                       </q-list>
                     </q-menu>
                   </q-btn>
                 </div>
               </div>
             </q-card-section>

             <q-card-section>
             </q-card-section>

             <q-separator />

             <q-card-actions>
               <q-btn flat color="ctmSage">Approve Hours</q-btn>
               <q-btn flat color="ctmSage">View Hour Totals</q-btn>
             </q-card-actions>
           </q-card>

</div>



  <!-- join/create expansion item -->
<div class= "absolute-bottom-right q-pr-lg q-pb-lg">
    <q-fab
    direction="up"
    color= "ctmGrey"
    text-color="ctmSage"
    icon="add"
    vertical-actions-align = "center">
          <q-fab-action color="ctmGrey"  text-color="ctmSage" @click="create" label="Create" />
          <q-fab-action color="ctmGrey"  text-color="ctmSage" @click="join" label="Join" />
      </q-fab>

</div>
</amplify-authenticator>
  </q-page>
</template>

<script>
import { API, Auth } from 'aws-amplify';
import { useQuasar } from 'quasar'
import { defineComponent, ref } from 'vue';
import CreateDialog from "src/components/CreateDialog.vue"
import { listUsers } from '../graphql/queries';



export default defineComponent({
  name: 'PageIndex',
  setup(){
    const user = Auth.currentAuthenticatedUser().then(user =>
    API.graphql({
      query:`
        query ListUsers(
          $filter: ModelUserFilterInput
          $limit: Int
          $nextToken: String
        ) {
          listUsers(filter: $filter, limit: $limit, nextToken: $nextToken) {
            items {
              id
              email
              fullname
              grade
              createdAt
              updatedAt
            }
            nextToken
          }
        }
      `,
      variables: {
        filter: {
          email: {
            eq: user.attributes.email
          }
        }
      }
    }).then(resp => {
      console.log(resp)
    }))
    const $q = useQuasar()
    const formTgl = ref('join')
    const secondModel = ref('one')
    const jCode = ref("")
    const groupName = ref("")

    const create = () => {
      $q.dialog({
        component: CreateDialog
       }).onOk(data => {
         // console.log('>>>> OK, received', data)
       })
    }

    const join = () => {
      $q.dialog({
        title: 'Join a Group',
        message: 'Join Code:',
        prompt: {
          model: '',
            isValid: val => val.length > 5,
            type: 'text' // optional
        },
        cancel: true,
        persistent: false
      }).onOk(data => {
        // console.log('>>>> OK, received', data)
      }).onCancel(() => {
        // console.log('>>>> Cancel')
      }).onDismiss(() => {
        // console.log('I am triggered on both OK and Cancel')
      })
    }

    return{
      fab1: ref(true),
      fab2: ref(true),
      create,
      join,
      formTgl,
      jCode,
      groupName
    }
  }



})
</script>

<style lang="scss">
  .homeform{
    width: 100%;
    height: 100%
  }
  body{
    background-color: #ffffff;
  }

// grey  custom color:
.text-ctmGrey{
  color: #a5d6a7;
}
.bg-ctmGrey {
  background: #a5d6a7;
}

// sage custom color
.text-ctmSage{
  color: #ffffff;
}
.bg-ctmSage{
  background:#ffffff;
}


</style>
