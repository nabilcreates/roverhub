<template>
        <StackLayout>

            <Label textWrap='true'>Max Martian Sol: {{max_sol}}</Label>

            <TextField v-model="value" />
            <Slider value="max_sol" v-model="value" minValue='0' :maxValue='max_sol' />
            <Button @tap="getApiData(value)">Get Pictures</Button>

            <StackLayout v-if="loadedAPI">

                <!-- DISPLAY THIS IF APIDATA.PHOTOS.LENGTH = 0 OR IN OTHER WORDS, NO PICS ON THAT SOL -->
                <Label textWrap='true' v-if="apiData.photos.length == 0">No Pics :(</Label>

                <ListView class="list-group" for="data in apiData.photos" @itemTap="onItemTap" style="height:1250px">
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



        </StackLayout>
</template>

<script>
    var appconfig = require("../package.json")
    var utilsModule = require("tns-core-modules/utils/utils");

    export default {
        data() {
            return {

                app: {
                    name: "",
                    version: "",
                },

                value: 2218,
                max_sol: "",

                api_key: "0Ls3Ro5l2tWOuHLvK3N8roehpIZxpYxIuK0WN9AZ",
                apiData: [],
                apiDateData: "",

                loadedAPI: false,
                loadedDate: false,

                sol: ""
            }
        },

        methods: {

            getLatestSol() {

                this.loadedDate = false;

                fetch("https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?sol=100&page=1&api_key=" + this.api_key)
                    .then(res => res.json())
                    .then(json => {

                        this.loadedDate = true;

                        if (this.loadedDate) {
                            this.apiDateData = json

                            // SOL = json.photos[0].rover.max_sol
                            // SET VALUE TO LATEST SOL
                            this.max_sol = json.photos[0].rover.max_sol
                        }
                    })

            },

            getApiData(solnum) {

                console.log(solnum)
                console.log("getting api")

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
            this.getLatestSol();
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

    Label {
        color: white;
    }

    Page {
        background-color: #161616;
        color: white;
    }

    Button {
        margin: 10 0;
        color: white;
        background-color: #d83131;
        border-radius: 1000;
        height: 38;
    }
</style>