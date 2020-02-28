<template>
    <div class="main">
        <v-container fluid>
            <v-row
                class="mb-6"
                no-gutters

                v-for="loop in 3"
                :key="loop"

            >

                <v-col
                v-for="(video, number) in listOfVideo"
                :key="number"
                >
                    <v-card max-width="400" class="mx-auto all" height="390px">
                        <v-img height="200" width="100%" :src="video.lien_img"></v-img>
                        
                        <div class="video">
                            <v-card-title :class="[selectedCountry === 'ES' ? disabledClass : '']" class="titre">
                                {{video.titre}}
                            </v-card-title>

                            <v-card-subtitle :class="[selectedCountry === 'ES' ? disabledClass : '']" class="titre">
                                {{video.description}}
                            </v-card-subtitle>
                        </div>
                    </v-card>

                </v-col>
            </v-row>
        </v-container>


        <v-dialog v-model="dialog" persistent max-width="600px" transition="scroll-y-transition">
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
            <span class="headline">Ajouter une nouvelle vidéo</span>
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
                    label="Tags"
                    multiple
                    ></v-autocomplete>
                </v-col>
                </v-row>
            </v-container>
            <small>*champs requis</small>
            </v-card-text>
            <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="error" @click="dialog = false">Annuler</v-btn>
            <v-btn color="primary" @click="openSnack">Publier</v-btn>
            </v-card-actions>
        </v-card>
        </v-dialog>

        <v-snackbar
         v-model="snackbar"
        :timeout="timeout"
        >
      {{ text }}
        </v-snackbar>


        <v-menu
            transition="slide-y-transition"
            bottom
            class="lang"
            >
            <template v-slot:activator="{ on }">
                    <p v-on="on" class="lang">{{selectedCountry}}</p>
                </template>
                <v-list>
                    <v-list-item
                    v-for="(country, index) in listCountry"
                    :key="index"
                    @click="selectCountry(country)"
                    >
                    <v-list-item-title>{{ country }}</v-list-item-title>
                    </v-list-item>
                </v-list>
            </v-menu>

    </div>
</template>


<script>
export default {
    
    data() {
        return {
            dialog: false,

            snackbar: false,
            text: 'Votre vidéo est en cours de publication.',
            timeout: 2000,


            listOfVideo: [
                {
                    titre: "Je vais supprimer cette vidéo dans 3 jours, désolé.",
                    description: "ABONNE-TOI ! http://bit.ly/2fm88Xo (merci) Vêtements Yoko : http://www.yokoshop.com Réseaux : Insta : https://www.instagram.com/xsqueezie/ Twitter : http://www.twitter.com/xSqueeZie Facebook...",
                    lien_img:"https://i.ytimg.com/vi/QAvLzYzJulc/hqdefault.jpg?sqp=-oaymwEZCNACELwBSFXyq4qpAwsIARUAAIhCGAFwAQ==&rs=AOn4CLDnLuhgdnP9HHfWdLm2xJswl0lJBQ",
                    country:"FR"
                },
                {
                    titre: "Taylor Swift - The Man (Official Video)",
                    description: "Official music video by Taylor Swift performing “The Man” – off her album ‘Lover.’ ",
                    lien_img:"https://i.ytimg.com/vi/AqAJLh9wuZ0/hqdefault.jpg?sqp=-oaymwEZCNACELwBSFXyq4qpAwsIARUAAIhCGAFwAQ==&rs=AOn4CLCTjpS_URuBZzTz1xSIzy9JydrJJQ",
                    country:"ES"
                },
                {
                    titre: "Le Jeu qui fait vomir ft. Léna Situations et Benjamin Tranié",
                    description: "Abonnez-vous pour d'autres vidéos de ce type et lâchez un pouce bleu ça fait toujours plaisir. ",
                    lien_img:"https://i.ytimg.com/vi/BDv_F_Ns-oE/hqdefault.jpg?sqp=-oaymwEZCNACELwBSFXyq4qpAwsIARUAAIhCGAFwAQ==&rs=AOn4CLAmt8yWqf1MxwuYy6E5TuLOMHSPDg",
                    country:"EN"
                },
                {
                    titre: "BTS Carpool Karaoke",
                    description: "James Corden hits the carpool lane with international superstars BTS to sing songs off their new album ",
                    lien_img:"https://i.ytimg.com/vi/T4x7sDevVTY/hqdefault.jpg?sqp=-oaymwEZCPYBEIoBSFXyq4qpAwsIARUAAIhCGAFwAQ==&rs=AOn4CLDl229Sdcx3l9Ysp663lW_juLPtSg",
                    country:"FR"
                },
            ],

           listCountry: [
                "EN",
                "FR",
                "ES"
            ],
            selectedCountry: "FR",
            disabledClass: 'disabled'
 
        }
    },

    methods:{
        openSnack: function(){
            this.dialog = false;

            this.snackbar = true;

        },
        
        selectCountry: function(country){
            console.log(country)
            this.selectedCountry = country
        }
    }


}
</script>


<style>
    
    .main{
        margin-top: 5%;
        background-color: rgb(206, 202, 202);
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

    .lang{
        padding: 2%;
        margin-top:1%;
        font-weight: bold;
        font-size: 20px;
        cursor: pointer;
        color: white;

        position: fixed;
        top: -33px;
        left: 43%;
        z-index: 100;
    }

    .titre{
        cursor: pointer;
    }

    .disabled{
        color: grey;
        cursor:default !important;
    }
    
</style>