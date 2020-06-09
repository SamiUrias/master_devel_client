<template>
  <div class="home">
    <div class="container">
      <div class="row d-flex justify-content-center">
        <b-form>
          <b-form-row>
            <label class="mr-sm-2" for="inline-form-custom-select-pref"
              >Key</label
            >
            <b-input v-model="key"></b-input>
          </b-form-row>

          <b-form-row>
            <label class="mr-sm-2">Shared Secret</label>
            <b-input v-model="shared_secret"></b-input>
          </b-form-row>

          <b-form-row>
            <b-button
              class="mt-3 w-100"
              variant="primary"
              @click="putCredentials"
              >PUT</b-button
            >
          </b-form-row>

          <!-- Response -->
          <b-form-row class="mt-5">
            <label class="mr-sm-2 font-weight-bolder">Response</label>
            <b-textarea class="" v-model="response"></b-textarea>
          </b-form-row>
        </b-form>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from "axios";
export default {
  name: "Home",
  data: function () {
    return {
      key: "",
      shared_secret: "",
      response: "",
    };
  },
  methods: {
    async putCredentials() {
      console.log("Putting...");
      console.log(process.env.VUE_APP_HOST);
      const response = await axios.put(
        process.env.VUE_APP_HOST + "/credentials",
        {
          key: this.key,
          shared_secret: this.shared_secret,
        }
      );
    },
  },
  components: {},
};
</script>
