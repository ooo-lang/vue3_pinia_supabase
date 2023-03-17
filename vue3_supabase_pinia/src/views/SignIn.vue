<script setup>
import { ref } from 'vue';
import { supabase } from '../supabase';
import { useRouter } from 'vue-router';

const router = useRouter();

const loading = ref(false)
const email = ref('');
const password = ref('');
const handleSubmit = async () => {
  try {
    loading.value = true
    const { error } = await supabase.auth.signInWithPassword({
      email: email.value,
      password: password.value,
    });

    if (error) throw error;
    
    router.push({
      name: 'dashboard',
    });
  } catch (error) {
    alert(error.massage);
    console.log(error);
  } finally {
    loading.value = false
  }
};
</script>
<template>
  <div>
    <h1>SignIn</h1>
    <form @submit.prevent="handleSubmit">
      <div>
        <label for="email">Email: </label>
        <input type="email" placeholder="email" v-model="email" />
      </div>
      <div>
        <label for="password">Password: </label>
        <input type="password" placeholder="password" v-model="password" />
      </div>
      <div>
        <input 
          type="submit"
          :value="loading ? 'Loading' : 'SignIn'"
          :disabled="loading" 
        />
      </div>
    </form>
  </div>
</template>