<template>

    <Page>

        <ActionBar :title="'Pictures'" />

        <StackLayout>

                <!-- DISPLAY THIS IF APIDATA.PHOTOS.LENGTH = 0 OR IN OTHER WORDS, NO PICS ON THAT SOL -->
                <Label textWrap='true' v-if="loadedAPI && apiData.photos.length == 0">No Pics :(</Label>

                <ListView v-if="loadedAPI" class="list-group" for="data in apiData.photos" @itemTap="onItemTap" style="height:1250px">
                    <v-template>
                        <StackLayout flexDirection="row" class="list-group-item">
                            <!-- DISPLAY THE IMAGE -->
                            <Image :src="data.img_src" />

                            <!-- DISPLAY DATE OF PHOTO TAKEN -->
                            <Label textWrap='true'>📅: {{data.earth_date}}</Label>
                            <Label textWrap='true'>📷: {{data.camera.full_name}} ({{data.camera.name}})</Label>

                        </StackLayout>
                    </v-template>
                </ListView>


        </StackLayout>
    </Page>
</template>

<script>
    var appconfig = require("../package.json")
    var utilsModule = require("tns-core-modules/utils/utils");

    export default {
        
        props: ['solnumber'],
        
        data() {
            return {

                app: {
                    name: "",
                    version: "",
                },

                max_sol: "",

                api_key: "0Ls3Ro5l2tWOuHLvK3N8roehpIZxpYxIuK0WN9AZ",
                apiData: [],

                loadedAPI: false,
            }
        },

        methods: {
            getApiData(solnum) {

                console.log("getting api")

                console.log(solnum)
                
                this.loadedAPI = false;
                fetch("https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?sol=" + solnum + "&api_key=" +
                        this.api_key)
                    .then(res => res.json())
                    .then(json => {
                        this.apiData = json;
                        this.loadedAPI = true;
                        console.log("done")
                    })

            },

            onItemTap(args) {
                var index = args.index
                console.log(index)
                utilsModule.openUrl(this.apiData.photos[args.index].img_src)
            }

        },

        mounted() {
            this.getApiData(this.solnumber)
        }

    }
</script>

<style scoped>
    /* ABC */
    /* PCOLOR IS #d83131 */

    ActionBar {
        background-color: #d83131;
        color: #ffffff;
    }

    StackLayout {
        margin: 0 10;
    }

    Page {
        background-color: white;
        color: black;
    }

    Button {
        margin-top: 10;
        color: white;
        background-color: #d83131;
        border-radius: 1000;
        height: 38;
    }
</style>