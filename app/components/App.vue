<template>
    <Page>
        <ActionBar :title="app.name + ' ' + app.version" />

        <TabView android:tabBackgroundColor="#ee6f1a" android:tabTextColor="#ffffff" android:selectedTabTextColor="#ffffff" androidSelectedTabHighlightColor="#ffffff">

            <TabViewItem title="Pictures">
                <pictures-vue />
            </TabViewItem>

            <TabViewItem title="About The Curiosity">
                <about-curiosity-vue />
            </TabViewItem>


        </TabView>



    </Page>
</template>

<script>
    var appconfig = require("../package.json")
    import PicturesVue from './Pictures.vue';
    import AboutCuriosityVue from './AboutCuriosity.vue';
    import HomeVue from './Home.vue'
    
    export default {

        components: {
            PicturesVue,
            AboutCuriosityVue,
            HomeVue,
        },

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
            },

            navigateToAboutCuriosity() {
                this.$navigateTo(AboutCuriosityVue)
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
    /* PCOLOR IS #ee6f1a */

    ActionBar {
        background-color: #ee6f1a;
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
        margin: 10 0;
        color: white;
        background-color: #ee6f1a;
        border-radius: 1000;
        height: 40;
    }
</style>