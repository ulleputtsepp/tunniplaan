<template>
    <Page class="page">
        <ActionBar title="Home" class="action-bar" />

        <ListView class="list-group" for="tund in tunnid" @itemTap="onItemTap"
            style="height: 1250px">
            <v-template>
                <FlexboxLayout flexDirection="row" class="list-group-item">

                    <!--Add your page content here-->
                    <Label :text="tund.opetaja" class="list-group-item" style="width: 60%" />
                    <Label :text="tund.aine" class="list-group-item" style="width: 60%" />
                </FlexboxLayout>
            </v-template>
        </ListView>
    </Page>
</template>

<script>
    const http = require("tns-core-modules/http");

    export default {
        data() {
            return {
                tunnid: []
            };
        },
        created() {
            this.getMySchedule();
        },
        methods: {
            getMySchedule() {
                var url =
                    "https://tkhk.siseveeb.ee/veebilehe_andmed/tunniplaan?nadal=2019-02-04&grupp=1223";
                http.request({
                    url: url,
                    method: "GET"
                }).then(this.parseResponse);
            },
            parseResponse(response) {
                var schedule = response.content.toJSON();
                this.tunnid = schedule["tunnid"]["2019-02-04"];
                console.log(tunnid);
            }
        }
    };
</script>

<style scoped>
    .home-panel {
        vertical-align: center;
        font-size: 20;
        margin: 15;
    }

    .description-label {
        margin-bottom: 15;
    }
</style>