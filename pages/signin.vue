<template>
  <div>
    <h1>Sign In</h1>
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

      <button type="submit">Sign In</button>
    </form>
    <h1 v-if="user">Welcom {{ user }}</h1>
  </div>
</template>

<script>
import { createClient } from "@supabase/supabase-js";

// Create a single supabase client for interacting with your database
const SUPABASE_URL = "https://hzfsuqxfngnxwfjlmavq.supabase.co";

const SUPABASE_KEY =
  "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJyb2xlIjoiYW5vbiIsImlhdCI6MTYxMjU4NjU3MywiZXhwIjoxOTI4MTYyNTczfQ.E8UBHVQVTjSKvcOuPHGQOnxufsiRNXz5tkJtueIELkA";
const supabase = createClient(SUPABASE_URL, SUPABASE_KEY);
export default {
  data() {
    return {
      email: "",
      password: "",

      name: this.name,
      valid: false,
      user: ""
    };
  },
  methods: {
    async signUp() {
      const { user, error } = await supabase.auth.signIn({
        email: this.email,
        password: this.password,
        name: this.name
      });

      this.valid = true;

      console.log(user);
      this.update();
    },
    async update() {
      const { user, error } = await supabase.auth.update({
        data: { name: this.name }
      });
   
      this.next();
    },
    next(){
        this.$router.push({name: 'dash'})
    }
  }
};
</script>

<style lang="scss" scoped></style>
