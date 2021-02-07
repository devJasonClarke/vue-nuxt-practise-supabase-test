<template>
  <div class="container">
    <h1>hello</h1>
    <div v-for="(post, index) in titles" :key="index">
      <h1>{{ post.title }}</h1>
      <p>{{ post.info }}</p>
    </div>
    <h2>{{ newVal }}</h2>
  </div>
</template>

<script>
import { createClient } from "@supabase/supabase-js";

// Create a single supabase client for interacting with your database
const supabaseUrl = "https://hzfsuqxfngnxwfjlmavq.supabase.co";

const supabaseKey =
  "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJyb2xlIjoiYW5vbiIsImlhdCI6MTYxMjU4NjU3MywiZXhwIjoxOTI4MTYyNTczfQ.E8UBHVQVTjSKvcOuPHGQOnxufsiRNXz5tkJtueIELkA";
const supabase = createClient(supabaseUrl, supabaseKey);
export default {
  data() {
    return {
      titles: [],
      newVal: "",
      testArray: []
    };
  },
  methods: {
    async name() {
      const { data, error } = await supabase.from("post").select();

      this.titles = data;
    },

    realtime() {
      const mySubscription = supabase
        .from("post")
        .on("UPDATE", payload => {
          console.log("Change received!", payload.new.id);
          console.log(this.titles);

          const update = this.titles.find(
            element => element.id === payload.new.id
          );
          const updateIndex = this.titles.findIndex(
            element => element.id === payload.new.id
          );
          const newValueIndex = update;
          this.titles = this.titles.splice(updateIndex, 0, update);
          console.log(newValue);
          this.newVal = newValue;

          const newValue = update;
          console.log(newValue);
          console.log(this.titles);
          this.newVal = newValue;
        })
        .subscribe();
    }
  },
  created() {
    this.name();
    this.realtime();
  }
};
</script>

<style></style>
