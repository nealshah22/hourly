<template>
  <q-page class = "q-pa-md">

    <!-- Example Group Card Member-->
       <q-card flat bordered class="my-card bg-grey-1">
             <q-card-section>
               <div class="row items-center no-wrap">
                 <div class="col">
                   <div class="text-h6 text-weight-bolder" style="font-size: 20pt">
                     Example Group
                   </div>
                   <div class="text-subtitle2">Member</div>
                 </div>

                 <div class = "col-5">

                     <div class="text-h4 text-weight-bold text-center"  style="font-size: 40pt">
                       12
                     </div>
                     <div class="text-subtitle2 text-center">
                       hours
                     </div>

                  </div>
                  <!-- center "hours" below "12" -->


                 <div class="col-auto">
                   <q-btn color="grey-7" round flat icon="more_vert">
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
               <q-btn flat>Submit Hours</q-btn>
               <q-btn flat></q-btn>
             </q-card-actions>
           </q-card>

    <!-- Example Group Card Owner-->
       <q-card flat bordered class="my-card bg-grey-1">
             <q-card-section>
               <div class="row items-center no-wrap">
                 <div class="col">
                   <div class="text-h6 text-weight-bolder" style="font-size: 20pt">
                     Example Group
                   </div>
                   <div class="text-subtitle2">Owner</div>
                 </div>
                 <div class = "col-5">
                   <div class="text-h4 text-weight-bold text-center"  style="font-size: 40pt">
                     12
                   </div>
                   <div class="text-subtitle2 text-center">
                     hours
                   </div>
                  </div>

                 <div class="col-auto">
                   <q-btn color="grey-7" round flat icon="more_vert">
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
               <q-btn flat>Approve Hours</q-btn>
               <q-btn flat>View Hour Totals</q-btn>
             </q-card-actions>
           </q-card>


  <!-- Toggle between join and create group -->
     <q-btn-toggle
       v-model="formTgl"
       spread
       no-caps
       rounded
       unelevated
       toggle-color="green-5"
       color="white"
       text-color="black"
       :options="[
         {label: 'Join a Group', value: 'join'},
         {label: 'Create a Group', value: 'create'}
       ]"
     />


<!-- create group form -->
     <div class="column justify-center items-center homeform" >
     <q-form v-if = "formTgl == 'create'">
       <q-input color="green"  filled v-model="groupName" label="Group Name">
         <template v-slot:prepend>
         </template>
       </q-input>
     </q-form>

<!-- join group form -->
     <q-form v-else>
       <q-input color="green"  filled v-model="jCode" label="Join Code">
        <template v-slot:prepend>
        </template>
      </q-input>
    </q-form>
  </div>

  <!-- join/create expansion item -->
<div class= "absolute-bottom-right q-pr-xl q-pb-xl">
    <q-fab
    direction="up"
    color="green"
    text-color="white"
    icon="add"
    vertical-actions-align = "center">
          <q-fab-action color="green"  text-color="white" @click="onClick" label="Create" />
          <q-fab-action color="green"  text-color="white" @click="onClick" label="Join" />
      </q-fab>

</div>

  </q-page>
</template>

<script>
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'PageIndex',
  setup(){
    const formTgl = ref('join')
    const secondModel = ref('one')
    const jCode = ref("")
    const groupName = ref("")
    return{
      fab1: ref(true),
      fab2: ref(true),
      onClick () {
        console.log('Clicked on a fab action')
      },
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
</style>
