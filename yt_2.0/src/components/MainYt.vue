<template>
    <div class="main">
        <v-container fluid>
            <v-row
                class="mb-6"
                no-gutters

                v-for="i in 4"
                :key="i"
            >

                <v-col
                    v-for="n in 4"
                    :key="n"
                >
                    <v-card max-width="300" class="mx-auto all" height="310px" min-height="310px" max-height="310px">
                        <v-img height="150" width="100%" src="https://cdn.vuetifyjs.com/images/cards/cooking.png"></v-img>
                        
                        <div class="video">
                            <v-card-title>
                                TITRE DE VIDEO
                            </v-card-title>

                            <v-card-subtitles>
                                Lorem, ipsum dolor sit amet consectetur adipisicing elit. Repellat laborum iste saepe dignissimos, consectetur
                            </v-card-subtitles>
                        </div>
                    </v-card>

                </v-col>
            </v-row>
        </v-container>

        <v-dialog v-model="dialog" persistent max-width="600px">
        <template v-slot:activator="{ on }">        
            <v-btn
            color="red"
            fab
            large
            dark
            bottom
            left
            class="v-btn-flottant"
            v-on='on'
            >
                <v-icon>mdi-plus</v-icon>
            </v-btn>
        </template>
        <v-card>
            <v-card-title>
            <span class="headline">Ajouter une nouvelle Vidéo</span>
            </v-card-title>
            <v-card-text>
            <v-container>
                <v-row>
                <v-col cols="12">
                    <v-text-field label="Titre de la vidéo*" required></v-text-field>
                </v-col>
                <v-col cols="12">
                    <v-text-field label="Description de la vidéo*" required></v-text-field>
                </v-col>
                <v-col cols="12">
                    <v-text-field label="Lien de la miniature*" required></v-text-field>
                </v-col>
                <v-col cols="12" sm="6">
                    <v-autocomplete
                    :items="['Gaming', 'Vlog', 'Degustation en couple.........', 'sport']"
                    label="Interests"
                    multiple
                    ></v-autocomplete>
                </v-col>
                </v-row>
            </v-container>
            <small>*champs requis</small>
            </v-card-text>
            <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="blue darken-1" text @click="dialog = false">Close</v-btn>
            <v-btn color="blue darken-1" text @click="dialog = false">Save</v-btn>
            </v-card-actions>
        </v-card>
        </v-dialog>



    </div>
</template>


<script>
export default {
    
    data() {
        return {
            dialog: false,
        }
    },


}
</script>


<style>
    
    .main{
        margin-top: 5%;
    }
    .video{
        padding: 20px;
    }
    .all{
        overflow: hidden;
    }
    .v-btn-flottant{
        position: fixed;
        bottom: 5%;
        right: 5%;
    }
    
</style>