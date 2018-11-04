<template>

    <StackLayout>

        <StackLayout v-if='loadedDate'>
            <Label class="h2" textWrap='true'>Loading of pictures may take up to 2 minutes!</Label>

            <GridLayout columns="*,*" rows='*' height='30'>
                <Label style='verticalAlignment: middle;' col='0' rows='0' textWrap='true'>Max Martian Sol: {{max_sol}}</Label>
                <Label style='verticalAlignment: middle;' col='1' rows='0' textWrap='true'>Current Martian Sol: {{value}}</Label>
            </GridLayout>

            <!-- <Slider value="max_sol" v-model="value" minValue='0' :maxValue='max_sol' /> -->

            <GridLayout columns="*,5*,*" rows="*" height="50">
                <Button style='border-radius: 0;' @tap="value --" col="0" row='0'>-</Button>
                <TextField v-model="value" col='1' row='0' />
                <Button style='border-radius: 0;' @tap="value ++" col='2' row='0'>+</Button>
            </GridLayout>

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

                api_key: "0Ls3Ro5l2tWOuHLvK3N8roehpIZxpYxIuK0WN9AZ",

                value: 0,
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
        background-color: #161616;
        color: white;
    }

    .h1,.h2,.h3,.h4,.h5,.h6{
        color: white;
    }

    Label{
        color:white;
    }
    Button {
        margin-top: 10;
        color: white;
        background-color: #d83131;
        border-radius: 1000;
        height: 38;
    }
</style>