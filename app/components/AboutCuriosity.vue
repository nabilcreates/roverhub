<template>
        <ScrollView>

            <StackLayout>
                <Image src="https://www.nasa.gov/sites/default/files/styles/full_width_feature/public/thumbnails/image/pia19808-main_tight_crop-monday.jpg" />

                <Label class='h1' style="color: white; font-weight: 700;" textWrap='true'>Curiosity</Label>

                <Label textWrap='true'>Curiosity is a car-sized rover designed to explore Gale Crater on Mars as part of NASA's Mars Science Laboratory mission (MSL).Curiosity was launched from Cape Canaveral on November 26, 2011, at 15:02 UTC aboard the MSL spacecraft and landed on Aeolis Palus in Gale Crater on Mars on August 6, 2012, 05:17 UTC. The Bradbury Landing site was less than 2.4 km (1.5 mi) from the center of the rover's touchdown target after a 560 million km (350 million mi) journey. The rover's goals include an investigation of the Martian climate and geology; assessment of whether the selected field site inside Gale Crater has ever offered environmental conditions favorable for microbial life, including investigation of the role of water; and planetary habitability studies in preparation for human exploration.
                </Label>

                <Label textWrap='true'>Picture from: https://www.nasa.gov/jpl/msl/pia19808/looking-up-at-mars-rover-curiosity-in-buckskin-selfie</Label>
                <Label textWrap='true'>Info from: https://en.wikipedia.org/wiki/Curiosity_(rover)</Label>
            </StackLayout>

        </ScrollView>
</template>

<script>
    var appconfig = require("../package.json")
    import PicturesVue from './Pictures.vue';

    export default {
        data() {
            return {

                app: {
                    name: "",
                    version: "",
                },
            }
        },

        methods: {
            navigateToPictures() {
                this.$navigateTo(PicturesVue)
            }
        },

        mounted() {
            this.app.name = appconfig.name;
            this.app.version = appconfig.version;
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
        margin: 15;
    }

    Label {
        color: white;
    }

    Page {
        background-color: #161616;
        color: white;
    }

    Button {
        margin-top: 10;
        color: white;
        background-color: #d83131;
        border-radius: 1000;
        /* height: 38; */
    }
</style>