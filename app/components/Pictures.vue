<template>
        <StackLayout>

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

            <Label v-else>Loading Pictures... This may take around 10-60 seconds</Label>
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

                api_key: "0Ls3Ro5l2tWOuHLvK3N8roehpIZxpYxIuK0WN9AZ",
                apiData: [],
                apiDateData: "",

                loadedAPI: false,
                loadedDate: false,
            }
        },

        methods: {

            getLatestDate() {

                this.loadedDate = false;

                fetch("https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?sol=100&page=1&api_key=" + this.api_key)
                    .then(res => res.json())
                    .then(json => {

                        this.loadedDate = true;

                        if (this.loadedDate) {
                            this.apiDateData = json
                            console.log(this.apiDateData.photos[0].rover.max_date)

                            // RUN GETAPIDATA
                            this.getApiData()
                        }
                    })

            },

            getApiData() {
                this.loadedAPI = false;
                fetch("https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?earth_date=" + this.apiDateData
                        .photos[0].rover.max_date +
                        "&api_key=" + this.api_key)
                    .then(res => res.json())
                    .then(json => {

                        this.apiData = json;
                        this.loadedAPI = true;

                        console.log(json)
                    })

            },

            onItemTap(args){
                var index = args.index
                console.log(index)
                utilsModule.openUrl(this.apiData.photos[args.index].img_src)
            }

        },

        mounted() {
            // this.app.name = appconfig.name;
            // this.app.version = appconfig.version;

            this.getLatestDate()

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

    StackLayout{
        margin: 0 10;
    }
    
    Label{
        color: white;
    }
    
    Page{
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