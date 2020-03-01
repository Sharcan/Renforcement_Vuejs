<template>
    <div class="main">
        <p class="title">Vous êtes sur le compte de: {{selectedAccount | toUppercase}}</p>
        <v-container fluid>
            <v-row
                class="mb-6"
                no-gutters

                v-for="(user, index) in listAccount"
                :key="index"
            >

                <v-row v-for="loop in 3" :key="loop">
                    <v-col
                    v-for="(video, number) in user.listOfVideo"
                    :key="number"
                    
                    >
                        <v-card max-width="400" class="mx-auto all" height="390px" v-if="selectedAccount === user.user">
                            <div style="width: 100%; height: 100%;"  :class="[selectedCountry === video.country ? disabledClass : '']">
                                <v-img height="200" width="100%" :src="video.lien_img"></v-img>
                                
                                <div class="video">
                                    <v-card-title class="titre">
                                        {{video.titre}}
                                    </v-card-title>

                                    <v-card-subtitle class="titre">
                                        {{video.description}}
                                    </v-card-subtitle>
                                </div>
                            </div>
                        </v-card>

                    </v-col>
                </v-row>
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
                    <p v-on="on" class="lang">{{selectedCountry | toUppercase}}</p>
            </template>
            <v-list>
                <v-list-item
                v-for="(country, index) in listCountry"
                :key="index"
                @click="selectCountry(country)"
                >
                <v-list-item-title>{{ country | toUppercase}}</v-list-item-title>
                </v-list-item>
            </v-list>
        </v-menu>

    </div>
</template>


<script>
export default {
    
    props: {

        selectedAccount: String

    },

    data() {
        return {
            dialog: false,

            snackbar: false,
            text: 'Votre vidéo est en cours de publication.',
            timeout: 2000,

            listAccount:[
                {
                    user: "Nicolas",
                    lien_avatar: "https://lh3.googleusercontent.com/proxy/XNFC_MsPjhdxcFkIyIugRvNWDQjNVn2nSoHCwkP2zn16FWymLWwbApvtgtFz7DPLXXNZGC-0P_52oGEHebDHPqbI2gTJ2Nqk23tu-pzinc57Ubww198yqPZOdc5lntZjrGIgWVPR2vk9GTgCqA",
                    listOfVideo: [
                    {
                        titre: "Je vais supprimer cette vidéo dans 3 jours, désolé.",
                        description: "ABONNE-TOI ! http://bit.ly/2fm88Xo (merci) Vêtements Yoko : http://www.yokoshop.com Réseaux : Insta : https://www.instagram.com/xsqueezie/ Twitter : http://www.twitter.com/xSqueeZie Facebook...",
                        lien_img:"https://i.ytimg.com/vi/QAvLzYzJulc/hqdefault.jpg?sqp=-oaymwEZCNACELwBSFXyq4qpAwsIARUAAIhCGAFwAQ==&rs=AOn4CLDnLuhgdnP9HHfWdLm2xJswl0lJBQ",
                        country:"fr"
                    },
                    {
                        titre: "Taylor Swift - The Man (Official Video)",
                        description: "Official music video by Taylor Swift performing “The Man” – off her album ‘Lover.’ ",
                        lien_img:"https://i.ytimg.com/vi/AqAJLh9wuZ0/hqdefault.jpg?sqp=-oaymwEZCNACELwBSFXyq4qpAwsIARUAAIhCGAFwAQ==&rs=AOn4CLCTjpS_URuBZzTz1xSIzy9JydrJJQ",
                        country:"es"
                    },
                    {
                        titre: "Le Jeu qui fait vomir ft. Léna Situations et Benjamin Tranié",
                        description: "Abonnez-vous pour d'autres vidéos de ce type et lâchez un pouce bleu ça fait toujours plaisir. ",
                        lien_img:"https://i.ytimg.com/vi/BDv_F_Ns-oE/hqdefault.jpg?sqp=-oaymwEZCNACELwBSFXyq4qpAwsIARUAAIhCGAFwAQ==&rs=AOn4CLAmt8yWqf1MxwuYy6E5TuLOMHSPDg",
                        country:"en"
                    },
                    ]              
                },
                {
                    user: "Benjamin",
                    lien_avatar:"https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcTAP3wMY06MrCNznk576dHLWEkGRHzSdqRwx2v-V8GaRS2s0j6a",
                    listOfVideo: [
                        {
                            titre: "Taylor Swift - The Man (Official Video)",
                        description: "Official music video by Taylor Swift performing “The Man” – off her album ‘Lover.’ ",
                        lien_img:"https://i.ytimg.com/vi/AqAJLh9wuZ0/hqdefault.jpg?sqp=-oaymwEZCNACELwBSFXyq4qpAwsIARUAAIhCGAFwAQ==&rs=AOn4CLCTjpS_URuBZzTz1xSIzy9JydrJJQ",
                        country:"es"
                    },
                    {
                        titre: "Le Jeu qui fait vomir ft. Léna Situations et Benjamin Tranié",
                        description: "Abonnez-vous pour d'autres vidéos de ce type et lâchez un pouce bleu ça fait toujours plaisir. ",
                        lien_img:"https://i.ytimg.com/vi/BDv_F_Ns-oE/hqdefault.jpg?sqp=-oaymwEZCNACELwBSFXyq4qpAwsIARUAAIhCGAFwAQ==&rs=AOn4CLAmt8yWqf1MxwuYy6E5TuLOMHSPDg",
                        country:"en"
                    },
                    {
                        titre: "Je vais supprimer cette vidéo dans 3 jours, désolé.",
                        description: "ABONNE-TOI ! http://bit.ly/2fm88Xo (merci) Vêtements Yoko : http://www.yokoshop.com Réseaux : Insta : https://www.instagram.com/xsqueezie/ Twitter : http://www.twitter.com/xSqueeZie Facebook...",
                        lien_img:"https://i.ytimg.com/vi/QAvLzYzJulc/hqdefault.jpg?sqp=-oaymwEZCNACELwBSFXyq4qpAwsIARUAAIhCGAFwAQ==&rs=AOn4CLDnLuhgdnP9HHfWdLm2xJswl0lJBQ",
                        country:"fr"
                    },
                    ]              
                },
                {
                    user: "Antoine",
                    lien_avatar: "https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcS7Qe42BK70LjD5j2UUe5LKExgoaYgOx7qMU00n5H810iLP1Q-D",
                    listOfVideo: [
                    {
                        titre: "Taylor Swift - The Man (Official Video)",
                        description: "Official music video by Taylor Swift performing “The Man” – off her album ‘Lover.’ ",
                        lien_img:"https://i.ytimg.com/vi/AqAJLh9wuZ0/hqdefault.jpg?sqp=-oaymwEZCNACELwBSFXyq4qpAwsIARUAAIhCGAFwAQ==&rs=AOn4CLCTjpS_URuBZzTz1xSIzy9JydrJJQ",
                        country:"es"
                    },
                    {
                        titre: "Je vais supprimer cette vidéo dans 3 jours, désolé.",
                        description: "ABONNE-TOI ! http://bit.ly/2fm88Xo (merci) Vêtements Yoko : http://www.yokoshop.com Réseaux : Insta : https://www.instagram.com/xsqueezie/ Twitter : http://www.twitter.com/xSqueeZie Facebook...",
                        lien_img:"https://i.ytimg.com/vi/QAvLzYzJulc/hqdefault.jpg?sqp=-oaymwEZCNACELwBSFXyq4qpAwsIARUAAIhCGAFwAQ==&rs=AOn4CLDnLuhgdnP9HHfWdLm2xJswl0lJBQ",
                        country:"fr"
                    },
                    {
                        titre: "Le Jeu qui fait vomir ft. Léna Situations et Benjamin Tranié",
                        description: "Abonnez-vous pour d'autres vidéos de ce type et lâchez un pouce bleu ça fait toujours plaisir. ",
                        lien_img:"https://i.ytimg.com/vi/BDv_F_Ns-oE/hqdefault.jpg?sqp=-oaymwEZCNACELwBSFXyq4qpAwsIARUAAIhCGAFwAQ==&rs=AOn4CLAmt8yWqf1MxwuYy6E5TuLOMHSPDg",
                        country:"en"
                    },
                    ]              
                },
            ],
            
           listCountry: [
                "en",
                "fr",
                "es",
                "all"
            ],
            selectedCountry: "all",

            disabledClass: 'disabled',


            absolute: true,
            overlay: false,
 
        }
    },

    methods:{
        openSnack: function(){
            this.dialog = false;

            this.snackbar = true;

        },
        
        selectCountry: function(country){
            this.selectedCountry = country
        }
    },

    filters: {
        toUppercase: function(language){
            return language.toUpperCase();
        }
    }


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
        left: 92%; 
        bottom: 90%;
    }

    .lang{
        padding: 2%;
        margin-top:1.2%;
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
        background-color: rgb(180, 180, 180)
    }

    .title{
        margin-left: 4%;
    }
    
</style>