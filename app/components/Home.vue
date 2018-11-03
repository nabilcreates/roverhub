<template>
    <StackLayout>
        <Label textWrap="true" class="h1" style="color: white; font-weight: 700;">{{app.name}}</Label>
        <Label textWrap="true" class="h4" style="color: white; font-weight: 700;">This app gathers the latest pictures taken by NASA's Curiosity Rover</Label>
        <Label textWrap="true">The images may load slowly (this depends on your internet connection). I am not responsible for your data usage or anything that happens to your phone</Label>
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
            }
        },

        mounted(){
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