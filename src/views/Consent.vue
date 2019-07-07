<template>
    <div class="profile-page">
        <section class="section-profile-cover section-shaped my-0">
            <div class="shape shape-style-1 shape-primary shape-skew alpha-4">
                <span></span>
                <span></span>
                <span></span>
                <span></span>
                <span></span>
                <span></span>
                <span></span>
            </div>
        </section>
        <section class="section section-skew">
            <div class="container">
                <card shadow class="card-profile mt--300" no-body>
                    <div class="px-4">
                        <div class="row justify-content-center">
                            <div class="col-lg-3 order-lg-2">
                                <div class="card-profile-image">
                                    <a href="#">
                                        <img :src="getImgUrl()"  class="rounded-circle">
                                        <!--<img v-lazy="'img/theme/team-3-800x800.jpg'" class="rounded-circle">-->
                                    </a>
                                </div>
                            </div>
                            <!--<div class="col-lg-4 order-lg-3 text-lg-right align-self-lg-center">
                                <div class="card-profile-actions py-4 mt-lg-0">
                                    <base-button type="info" size="sm" class="mr-4">Connect</base-button>
                                    <base-button type="default" size="sm" class="float-right">Message</base-button>
                                </div>
                            </div>
                            <div class="col-lg-4 order-lg-1">
                                <div class="card-profile-stats d-flex justify-content-center">
                                    <div>
                                        <span class="heading">22</span>
                                        <span class="description">Friends</span>
                                    </div>
                                    <div>
                                        <span class="heading">10</span>
                                        <span class="description">Photos</span>
                                    </div>
                                    <div>
                                        <span class="heading">89</span>
                                        <span class="description">Comments</span>
                                    </div>
                                </div>
                            </div>-->
                        </div>
                        </br>
                        </br>

                        <div class="text-center mt-5">
                            <h3>Consent Management
                                <span class="font-weight-light"></span>
                            </h3>
                            </br>
                            <hr>

                            <div class="h4">Gathering the Data</div>
                            <div class="row">
                                <div class="col-md-2 h4 ">
                                </div>
                                <div class="col-md-8">
                                The more data collected, the stronger and more reliable the information will be for researchers to study.
                                For this reason, it is important to have as many participants as possible included in the Autoimmune Research Network (ARNet).
                                NCAPG members and other interested parties who want to join ARNet are welcome to create their own webpage on their own website to encourage participation.
                                </div>
                                <div class="col-md-2">
                                </div>
                            </div>

                        </div>

                        <hr>

                        <div class="h4">Using the data</div>
                            <div class="row">
                                <div class="col-md-2 h4 ">
                                </div>
                                <div class="col-md-8">
                                The data collected will be stored securely through Global Vision T echnologies.
                                When researchers want access to the information, they will contact ARNet. From that point, AARDA or the participating group will work with the researchers to provide them with the data, regardless of which organization the patients went through to submit their data.
                                The information will be used to gather patient experiences and help with autoimmune research.
                                Researchers and companies may make a contribution to the charity for access to the information.
                                </div>
                                <div class="col-md-2">
                                </div>
                            </div>

                        <div class="mt-5 py-5 border-top text-center">
                            <div class="row justify-content-center">
                                <div class="col-lg-9">
                                    <p>This is where you will be able to set up your preferences for granting and revoking access to third parties to share your data </p>
                                </div>
                            </div>
                            <hr>
                        </div>


                        <div>    <!-- Grid Div -->
                            <div class="row">
                                <div class="col-md-4">
                                    <label for="name"><h5> Your Unique Decentralized ID: </h5></label>
                                </div>
                                <div class="col-md-5">
                                    <base-input id="did" ref="didRef" type="text"></base-input>
                                </div>
                                <div class="col-md-3">

                                </div>
                            </div>
                        </div>

                        <hr>

                        </br>

                    </div>
                </card>
            </div>
        </section>
    </div>
</template>
<script>

    import { Connect } from 'uport-connect'

    export default {
        data() {
            return {

            }
        },
        mounted() {
            //this.loadWeb3Provider();  -> for dynamic change via dropdown
            this.getDidInfo();
        },
        methods: {
            getDidInfo: function () {

                const uport = new Connect('MyDApp')
                let did = localStorage.getItem("did")
                this.$refs.didRef.value = did

                //Get DID from uport profile
                // uport.requestDisclosure()

                // with uport-connect v.1.0.x get an error here that requestCredentials is not a function
                /*uport.requestCredentials({
                    requested: ["name", "avatar", "country"],
                    notifications: true
                    }).then((credentials) => {
                        console.log(credentials)
                })*/

            },
            getImgUrl: function() {

                //Now get it from uport profile
                const uport = new Connect('MyDApp')
                let imgUrl;

                // uport.requestDisclosure()
                // uport.onResponse('disclosureReq').then(res => {
                    if(uport.getImgUrl) {
                        imgUrl = uport.getImgUrl
                    }
                    else {
                        imgUrl = "img/theme/dna1.jpg";
                    }
                    return imgUrl;
               // })
                return imgUrl;
            }
        }
    };
</script>
<style>
</style>
