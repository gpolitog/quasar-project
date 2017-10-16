<template>
  <q-layout>
    <q-toolbar slot="header" class="toolbar">
      <q-toolbar-title :padding="0">
        Repositórios - Quasar Framework v{{ $q.version }}
      </q-toolbar-title>
    </q-toolbar>
    <div class="layout-padding">
      <h4>30 últimos repositórios</h4>
      <q-list highlight>
        <q-item v-for="repo in list">
          <q-item-side :avatar="repo.owner.avatar_url" />
          <q-item-main>
            <q-item-tile label>{{ repo.name }}</q-item-tile>
            <q-item-tile sublabel>{{ repo.html_url }}</q-item-tile>
          </q-item-main>
          <q-item-side right>
            <a :href="repo.html_url" target="_blank">
              <i class="material-icons">open_in_browser</i>
            </a>
          </q-item-side>
        </q-item>
      </q-list>
    </div>
  </q-layout>
</template>

<script>

import {
  QLayout,
  QToolbar,
  QToolbarTitle,
  QBtn,
  QIcon,
  QList,
  QListHeader,
  QItem,
  QItemSide,
  QItemMain,
  QItemTile
} from 'quasar'

import axios from 'axios'
let user = 'lauroguedes'

export default {
  components: {
  QLayout,
  QToolbar,
  QToolbarTitle,
  QBtn,
  QIcon,
  QList,
  QListHeader,
  QItem,
  QItemSide,
  QItemMain,
  QItemTile
  },
  data () {
    return {
      list: []
    }
  },
  mounted () {
    axios.get('https://api.github.com/users/' + user + '/repos?direction=asc')
      .then((res) => {
        this.list = res.data
        console.log(this.list)
      })
  }
}
</script>

<style>
</style>
