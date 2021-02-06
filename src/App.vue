<template>
  <div id="app">
    <notifications group="main" position="top center">
      <template slot="body" slot-scope="props">
        <div class="box" :style="{ 'margin-top': '8px' }">
          <div :class="`columns is-vcentered has-text-primary`">
            <div class="column">
              <div class="title is-5">{{ props.item.title }}</div>
            </div>
          </div>
        </div>
      </template>
    </notifications>
    <div class="columns is-vcentered">
      <div class="column is-5 is-offset-1">
        <section class="hero">
          <div class="hero-body">
            <figure class>
              <img src="@/assets/logo.jpeg" alt="password" />
            </figure>
          </div>
        </section>
      </div>
      <div class="column is-5">
        <section class="hero is-fullheight">
          <div class="hero-body">
            <div class="container">
              <div class="columns is-centered is-vcentered">
                <div class="column is-10">
                  <h1 class="title is-size-2">
                    Drop an idea in the box below, it's completely anonymous
                  </h1>
                  <br />
                  <div class="field">
                    <textarea
                      class="textarea is-large has-fixed-size"
                      placeholder="Your idea here..."
                      v-model="comment"
                    ></textarea>
                  </div>
                  <div class="field">
                    <div
                      class="button is-primary is-large has-text-white has-text-weight-bold is-fullwidth"
                      :disabled="!comment"
                      @click="submit"
                    >
                      Submit
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </section>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios"

export default {
  name: "App",
  data: function() {
    return {
      comment: "",
    }
  },
  methods: {
    async submit() {
      if (this.comment) {
        await axios.post(process.env.VUE_APP_SHEET, {
          data: [
            {
              comment: this.comment,
            },
          ],
        })
        this.$notify({
          group: "main",
          title: "Thanks! We've got your idea.",
        })
        this.comment = ""
      }
    },
  },
}
</script>

<style></style>
