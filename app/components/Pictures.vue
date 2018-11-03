<template>

    <StackLayout>

        <StackLayout v-if='loadedDate'>
            <Label textWrap='true'>Loading of pictures may take up to 2 minutes!</Label>
            <Label textWrap='true'>Max Martian Sol: {{max_sol}}</Label>
            <Label textWrap='true'>Current Martian Sol: {{value}}</Label>
            <TextField v-model="value" />
            <!-- <Slider value="max_sol" v-model="value" minValue='0' :maxValue='max_sol' /> -->

            <Button @tap="value -= 1">-</Button>
            <Button @tap="value += 1">+</Button>
            
            <Button @tap="navigateToViewPictures">Get Pictures</Button>
        </StackLayout>

    </StackLayout>

</template>

<script>
    var appconfig = require("../package.json")
    var utilsModule = require("tns-core-modules/utils/utils");
    import ViewPicturesVue from './ViewPictures.vue';


    export default {
        data() {
            return {

                api_key:  "0Ls3Ro5l2tWOuHLvK3N8roehpIZxpYxIuK0WN9AZ",
                
                value: 2218,
                max_sol: "",

                apiDateData: [],
                
                loadedDate: false,

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
                            this.loadedDate = true;
                            // SOL = json.photos[0].rover.max_sol
                            // SET VALUE TO LATEST SOL
                            this.max_sol = json.photos[0].rover.max_sol
                        }
                    })

            },

            navigateToViewPictures() {
                this.$navigateTo(ViewPicturesVue, {
                    props: {
                        'solnumber': this.value
                    }
                })

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