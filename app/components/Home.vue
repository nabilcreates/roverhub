<template>

    <ScrollView>
        <StackLayout>
            <Label textWrap="true" class="h1" >{{app.name}}</Label>
            <Label textWrap="true" class="h3" >This app gathers the latest pictures taken by NASA's Curiosity Rover</Label>
            <Label textWrap="true">The images may load slowly (this depends on your internet connection). I am not responsible for your data usage or anything that happens to your phone</Label>

            <Label textWrap="true" class="h2">Swipe To Continue ➡️</Label>

        </StackLayout>
    </ScrollView>

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

            }
        },

        mounted() {
            this.app.name = appconfig.name;
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
        margin: 20;
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

    .h1, .h2, .h3{
        font-weight: 700;
    }
    
    
</style>