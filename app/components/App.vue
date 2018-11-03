<template>
    <Page>
        <ActionBar :title="app.name + ' ' + app.version" />

        <TabView tabBackgroundColor="#d83131" androidTabsPosition="top" selectedTabTextColor="#ffffff">
            <TabViewItem title="Home">
                <home-vue />
            </TabViewItem>

            <TabViewItem title="Pictures From Curiosity">
                <pictures-vue />
            </TabViewItem>

            <TabViewItem title="About Curiosity">
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
        margin: 10 0;
        color: white;
        background-color: #d83131;
        border-radius: 1000;
        height: 38;
    }
</style>