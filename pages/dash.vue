<template>
    <div>
<h1>Hello! {{user}}</h1>
<img :src="img" :alt="user">
    </div>
</template>

<script>
import { createClient } from "@supabase/supabase-js";

// Create a single supabase client for interacting with your database
const SUPABASE_URL  = "https://hzfsuqxfngnxwfjlmavq.supabase.co";

const SUPABASE_KEY = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJyb2xlIjoiYW5vbiIsImlhdCI6MTYxMjU4NjU3MywiZXhwIjoxOTI4MTYyNTczfQ.E8UBHVQVTjSKvcOuPHGQOnxufsiRNXz5tkJtueIELkA";
const supabase = createClient(SUPABASE_URL, SUPABASE_KEY);
    export default {
        data() {
            return {
            user: "",
            img: ''
            }
        },
        methods: {
           async loadUser() {
                const user = await supabase.auth.user();
                this.user = user.user_metadata.full_name;
                this.img = user.user_metadata.avatar_url;
            console.log(user)
            }
        },
        created () {
            this.loadUser()
        },
    }
</script>

<style lang="scss" scoped>

</style>