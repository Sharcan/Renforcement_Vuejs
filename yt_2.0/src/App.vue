<template>
  <v-app class="all">

    <div>

        <v-navigation-drawer
            v-model="drawer"
            app
            clipped
            temporary
        >
            <v-list-item-group
                v-model="group"
                active-class="deep-purple--text text--accent-4"
            >
            
                <v-list-item-title class="collapse-title">Comptes Disponibles</v-list-item-title>
                <v-list-item v-for="(item, index) in elements" :key="index">
                    <v-list-item-title @click="selectAccount(item)"><v-icon middle color="black">mdi-account-circle</v-icon>{{item}}</v-list-item-title>
                </v-list-item>
            </v-list-item-group>

        </v-navigation-drawer>



        <v-app-bar
        color="red"
        dark
        fixed
        >
            <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>

            <v-toolbar-title>Youtube 2.0</v-toolbar-title>

            <v-spacer></v-spacer>

            <v-autocomplete
            label="Rechercher une vidéo"
            flat
            solo-inverted
            hide-details
            hide-selected
            class="search"

            v-model="select"
            :loading="loading"
            :items="items"
            :search-input.sync="search"
            >

            </v-autocomplete>

            
        </v-app-bar>

    </div>

    <MainYt :selectedAccount="selectedAccount"></MainYt>

  </v-app>
</template>

<script>
import MainYt from './components/MainYt';

export default {
  name: 'App',

  components: {
    MainYt
  },

data() {
        return {
            //Pour auto-completion
            loading: false,
            items: [],
            search: null,
            select: null,
            
            dataSearch: [
                "Cyprien",
                "Norman"
            ],

            //Pour collapse à gauche
            drawer: false,
            group: null,

            elements: [
              "Nicolas",
              "Antoine",
              "Benjamin"
            ],
            selectedAccount: 'Nicolas'

 
        }
    },

    watch: {
      search (val) {
        val && val !== this.select && this.querySelections(val)
      },
      group () {
        this.drawer = false
      },
    },
    methods: {
      querySelections (v) {
        this.loading = true
        // Simulated ajax query
        setTimeout(() => {
          this.items = this.dataSearch.filter(e => {
            return (e || '').toLowerCase().indexOf((v || '').toLowerCase()) > -1
          })
          this.loading = false
        }, 500)
      },

      selectAccount: function(account){
        this.selectedAccount = account
      }

    },
};
</script>


<style>
  .all{
    background-color: rgb(206, 202, 202);
  }

  .search{
    padding-top: 20px;
  }

  .collapse-title{
    font-size: 20px;
    padding: 20px;
  }

  
</style>