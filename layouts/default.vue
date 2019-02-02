<template>
  <v-app>
    <v-navigation-drawer v-model="drawer" absolute temporary>
      <v-list class="pa-1">
        <v-list-tile avatar>
          <v-list-tile-avatar>
            <img src="~static/csris_logo.png">
          </v-list-tile-avatar>

          <v-list-tile-content>
            <v-list-tile-title>CSRIS</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-list>

      <v-list class="pt-0" dense>
        <v-divider></v-divider>
        <v-list-tile v-for="item in items" :key="item.title" 
          @click.stop :to="item.route">
          <v-list-tile-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-tile-action>

          <v-list-tile-content>
            <v-list-tile-title>{{ item.title }}</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar fixed app>
      <v-toolbar-side-icon 
        @click.stop="drawer = !drawer"
        class="hidden-md-and-up">
      </v-toolbar-side-icon>
      <v-toolbar-title>CSRIS</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-toolbar-items class="hidden-sm-and-down">
        <v-btn v-for="item in items" :key="item.icon"
          flat :to="item.route">
          {{item.title}}
        </v-btn>
      </v-toolbar-items>
    </v-toolbar>
    <v-content>
      <v-container>
        <nuxt/>
      </v-container>
    </v-content>
    <v-footer dark height="auto">
      <v-card class="flex" flat tile>
        <v-card-actions class="justify-center">&copy;2019 —
          <strong>Cambridge Silk Road International School</strong>
        </v-card-actions>
      </v-card>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      drawer: null,
      items: [
        { title: 'Home', icon: 'dashboard', route: '/' },
        { title: 'About', icon: 'info', route: '/about' },
        { title: 'Primary', icon: 'accessibility_new', route: '/primary' },
        { title: 'Secondary 1', icon: 'directions_walk', route: '/secondary1' },
        { title: 'IGCSE', icon: 'directions_run', route: 'igcse' },
        { title: 'AS/A Level', icon: 'directions_bike', route: 'asanda' }
      ]
    }
  }
}
</script>
