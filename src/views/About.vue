<template>
    <div class="home">
        <div class="container">
            <div class="row d-flex justify-content-center">
                <b-form  class="w-100" style="border: 1px solid red">
                    <b-form-row>
                        <b-col>
                            <label class="mr-sm-2">x-key</label>
                            <b-input v-model="x_key"></b-input>
                        </b-col>
                        <b-col>
                            <label class="mr-sm-2">x-route</label>
                            <b-input v-model="x_route"></b-input>
                        </b-col>
                        <b-col>
                            <label class="mr-sm-2">x-signature</label>
                            <b-input v-model="x_signature"></b-input>
                        </b-col>
                    </b-form-row>

                    <b-form-row>
                        <b-col>
                            <label class="mr-sm-2">ID</label>
                            <b-input v-model="id"></b-input>
                        </b-col>
                        <b-col>
                            <label class="mr-sm-2">tag</label>
                            <b-input v-model="tag"></b-input>
                        </b-col>
                    </b-form-row>

                    <b-form-row>
                        <b-col>
                            <b-button class="mt-3 w-100" variant="primary" @click="getSingleMessage">Get tag messages</b-button>
                        </b-col>
                        <b-col>
                            <b-button class="mt-3 w-100" variant="primary" @click="getSingleTagMessages">Get id messages</b-button>
                        </b-col>
                    </b-form-row>
                    <b-form-row>
                        <b-col>
                            <b-button class="mt-3 w-100" variant="success" @click="singleMessagePost">Create</b-button>
                        </b-col>
                    </b-form-row>
                    <hr/>

                    <!-- Response -->
                    <b-form-row class="mt-5">
                        <label class="mr-sm-2 font-weight-bolder">Response</label>
                        <b-textarea class="" v-model="response"></b-textarea>
                    </b-form-row>
                    <b-form-row class="mt-5">
                        <label class="mr-sm-2 font-weight-bolder">Status</label>
                        <b-textarea class="" v-model="response_code"></b-textarea>
                    </b-form-row>
                </b-form>
            </div>


        </div>
    </div>
</template>

<script>
    // @ is an alias to /src
    import axios from 'axios'
    export default {
        name: "About",
        data: function (){
            return {
                x_key: "",
                x_route: "",
                x_signature:"",
                id: "",
                tag:"",
                response: "",
                response_code: ""
            }
        },
        methods: {
            async singleMessagePost() {
                try {
                    const response = await axios.post(process.env.VUE_APP_HOST + '/api/message/', {
                        id: this.id,
                        tag: this.tag
                    }, { headers: {
                            "x-key":this.x_key,
                            "x-route":this.x_route,
                            "x-signature":this.x_signature
                        }})

                    this.response_code = response.status

                } catch(error) {
                    this.response_code = error.response.status
                }
            },
            async getSingleMessage() {
                try {
                    const response = await axios.get(process.env.VUE_APP_HOST + '/api/message/'+this.id+'/',  { headers: {
                            "x-key":this.x_key,
                            "x-route":this.x_route,
                            "x-signature":this.x_signature
                        }})

                    this.response = response.data

                } catch(error) {
                    this.response_code = error.response.status
                }
            },
            async getSingleTagMessages() {
                try {
                    const response = await axios.get(process.env.VUE_APP_HOST + '/api/messages/'+this.tag+'/',  { headers: {
                            "x-key":this.x_key,
                            "x-route":this.x_route,
                            "x-signature":this.x_signature
                        }})

                    this.response = response.data

                } catch(error) {
                    this.response_code = error.response.status
                }
            },
        },
        components: {}
    };
</script>
