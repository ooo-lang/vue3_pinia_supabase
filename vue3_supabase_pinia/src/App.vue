<script setup>
import { supabase } from './supabase';
import { useAuthStore } from './stores/auth';
const auth = useAuthStore();
// const {
//   data: { session },
// } = await supabase.auth.getSession();
// const { user } = session;
// auth.setUser(user);
// auth.setUser(supabase.auth.getSession());

supabase.auth.onAuthStateChange((event, session) => {
  if (event == 'SIGNED_IN') auth.setUser(session.user);
  if (event == 'SIGNED_OUT') auth.clearUser();
});
</script>
<template>
    <router-view></router-view>
</template>
<style scoped>

</style>
