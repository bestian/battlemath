<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="leftDrawerOpen = !leftDrawerOpen"
        />

        <q-toolbar-title>
          數字對決
        </q-toolbar-title>

        <div>第1版</div>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      content-class="bg-grey-1"
    >
      <q-list>
        <q-input type="number" v-model = "d" 
        label="難度"/>
        <q-select
        filled
        v-model="multiple"
        multiple
        :options="options"
        label="算法"
        style="width: 250px"
      />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view :d = "d" :types="multiple" />
    </q-page-container>
  </q-layout>
</template>

<script>
export default {
  name: 'MainLayout',
  data () {
    return {
      leftDrawerOpen: false,
      d: 10,
      multiple: ['+', '-'],
      options: ['+', '-', '×']
    }
  }
}
</script>
