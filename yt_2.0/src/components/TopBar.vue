<template>
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
                <v-list-item v-for="(item, index) in elements" :key="index">
                    <v-list-item-title>{{item}}</v-list-item-title>
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
</template>



<script>

export default {
    
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
            ]
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
    },

}
</script>

<style>
    .search{
        padding-top: 20px;
    }
</style>