<template>

    <StackLayout>

        <StackLayout v-if='loadedDate'>
            <Label class="h3" textWrap='true' style="text-align: center; font-weight: 700; margin: 10 0;">Select a Martian Sol</Label>

            <GridLayout columns="*,*" rows='*' height='30'>
                <Label style='text-align: center;' col='0' rows='0' textWrap='true'>Max Martian Sol: {{max_sol}}</Label>
                <Label style='text-align: center;' col='1' rows='0' textWrap='true'>Current Martian Sol: {{value}}</Label>
            </GridLayout>

            <!-- <Slider value="max_sol" v-model="value" minValue='0' :maxValue='max_sol' /> -->

            <GridLayout columns="*,5*,*" rows="*" height="50">
                <Button @tap="value --" col="0" row='0'>-</Button>
                <TextField style="text-align: center;" v-model="value" col='1' row='0' />
                <Button @tap="value ++" col='2' row='0'>+</Button>
            </GridLayout>

            <Button @tap="navigateToViewPictures">Get Pictures</Button>
        </StackLayout>

        <Label v-else>Loading..</Label>

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
        color: white;
        background-color: #d83131;
    }

</style>