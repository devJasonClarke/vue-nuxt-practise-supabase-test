<template>
  <div>
    <h1>Sign Up</h1>
    <form @submit.prevent="signUp">
      <input type="text" name="" placeholder="name" id="" v-model="name" />
      <input type="email" name="" placeholder="email" id="" v-model="email" />
      <input
        type="text"
        name=""
        placeholder="password"
        id=""
        v-model="password"
      />
      <button type="submit">Sign Up</button>
    </form>
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
      email: "",
    name: '',
      password: "",
      valid: false
    };
  },
  methods: {
    async signUp() {
      const { user, error } = await supabase.auth.signUp({
        email: this.email,
        password: this.password,
         name: this.name,
      });
      this.valid = true;
      this.nextRoute();
    },
    nextRoute() {
      if (this.valid) {
        this.$router.push({ name: "signin" });
      }
    }
  }
};
</script>

<style lang="scss" scoped></style>
