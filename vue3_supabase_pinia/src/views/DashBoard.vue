<script setup>
import { supabase } from '../supabase';
import { useRouter } from 'vue-router';
const router = useRouter();

const handleSignOut = async () => {
  try {
    const { error } = await supabase.auth.signOut();
    if (error) throw error;
    router.push({
      name: 'home',
    });
  } catch (error) {
    alert(error.message);
  }
};
</script>
<template>
  <div>
    <div>
      <button @click="handleSignOut">SignOut</button>
    </div>
    <h1>DashBoard</h1>
    <p>Welcome to our service</p>
  </div>
</template>