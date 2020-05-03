<template>
  <section>
    <div class="container">
      <div class="row">
        <div class="col-md-4 offset-md-4">
          <div class="card p-4">
            <h1>Twilio App</h1>
            <form @submit.prevent="sendMessage">
              <div class="form-group">
                <label for="Number">Enter Phone Number</label>
                <input
                  v-model="message.to"
                  type="text"
                  placeholder="080********"
                  class="form-control"
                  required
                />
              </div>
              <div class="form-group">
                <label for="Number">Enter Message</label>
                <textarea
                  v-model="message.message"
                  class="form-control"
                  id
                  cols="30"
                  rows="10"
                  required
                ></textarea>
              </div>
              <button type="submit" class="btn btn-primary">
                <span
                  v-if="loading"
                  class="spinner-grow spinner-grow-sm"
                  role="status"
                  aria-hidden="true"
                ></span>Send
              </button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
<script>
import swal from "sweetalert";
import axios from "axios";
export default {
  data() {
    return {
      message: {
        to: "",
        message: ""
      },
      loading: false
    };
  },
  methods: {
    async sendMessage() {
      this.loading = true;
      try {
        let response = await axios.post(
          "http://localhost:3000/send-message",
          this.message
        );
        console.log(response);

        swal("Success", response.data.message, "success");
        this.loading = false;
      } catch (err) {
        swal("Error", "Something Went Wrong", "error");
        this.loading = false;
        console.log(err);
      }
    }
  }
};
</script>