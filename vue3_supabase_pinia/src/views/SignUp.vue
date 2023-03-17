<script setup>
import { ref } from 'vue';
import { supabase } from '../supabase';
// import router from '../router';
import { useRouter } from 'vue-router';
const router = useRouter();

const email = ref('');
const password = ref('');
const handleSubmit = async () => {
  try {
    const { error, user } = await supabase.auth.signUp({
      email: email.value,
      password: password.value,
    });
    if (error) throw error;
    if (user)
      router.push({
        name: 'emailConfirmation',
        query: { email: email.value },
      });
  } catch (error) {
    alert(error.message);
  }
  console.log('Email:', email.value);
  console.log('Password:', password.value);
};
</script>
<template>
  <h1>SignUp</h1>
  <form @submit.prevent="handleSubmit">
    <div>
      <label for="email">Email:</label>
      <input type="email" placeholder="email" v-model="email" />
    </div>
    <div>
      <label for="password">Password:</label>
      <input type="password" placeholder="password" v-model="password" />
    </div>
    <div>
      <button>SignUp</button>
    </div>
  </form>
</template>
<!-- <script>
export default {
  data() {
    return {
      email: '',
      password: '',
    }
  },
  methods: {
    handleSubmit() {
      console.log('Email:', this.email);
      console.log('Password:', this.password);
    }
  }
}
</script> -->