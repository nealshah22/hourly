<template>
  <q-page padding>
    <q-input dark dense standout v-model="text" input-class="text-right" class="q-ml-md">
          <template v-slot:append>
            <q-icon v-if="text === ''" name="search" />
            <q-icon v-else name="clear" class="cursor-pointer" @click="text = ''" />
          </template>
        </q-input>

        <q-list bordered class="rounded-borders" style="max-width: 600px">
    <q-item-label header>Google Inbox style</q-item-label>
<div
  v-for ="(i,group) in groups"
  :key="group.name"
>
    <q-item>
      <q-item-section avatar top>
        <q-icon name="account_tree" color="black" size="34px" />
      </q-item-section>

      <q-item-section top class="col-2 gt-sm">
        <q-item-label class="q-mt-sm">{{group.name}}</q-item-label>
      </q-item-section>

      <q-item-section top>
        <q-item-label lines="1">
          <span class="text-weight-medium">{{group.id}}</span>
        </q-item-label>
        <q-item-label caption lines="1">
          Total hours: {{group.totalHours}}
        </q-item-label>
      </q-item-section>

      <q-item-section top side>
        <div class="text-grey-8 q-gutter-xs">
          <q-btn class="gt-xs" size="12px" flat dense round icon="delete" />
          <q-btn class="gt-xs" size="12px" flat dense round icon="done" />
          <q-btn size="12px" flat dense round icon="more_vert" />
        </div>
      </q-item-section>
    </q-item>

    <q-separator spaced />
</div>
  </q-list>


  </q-page>
</template>

<script>
import { defineComponent, ref, watch } from 'vue';
export default defineComponent( {
  name: 'PageName',
  setup () {
    const text = ref("Search")
    const groups = ref([
      {
        name: "Red Cross Club",
        totalHours: 64,
        id: "aasdfasdf1231244"
      },
      {
        name: "Key Club",
        totalHours: 143,
        id: "asdf09830uasd90f80123"
      }
    ])
    return{
      text,
      groups
    }

  }
})
</script>
