<template>
    <header class="bg-at-light-green text-white ">
        <nav class="container py-5 px-4 flex flex-col gap-4 items-center sm:flex-row">
            <div class="flex items-center gap-x-4">
                
                <h1 class="text-lg">Open doors</h1>
            </div>
            <ul class="flex flex-1 justify-end gap-x-10">
                <router-link v-if="!user" :to="{name: 'LoginView'}" class="cursor-pointer">Login</router-link>
                <li v-if="user" @click="logout" class="cursor-pointer">Logout</li>
            </ul>
        </nav>

    </header>
  </template>
  
  <script>
  import store from '../store/index';
  import { computed } from 'vue';
  import { supabase } from '../supabase/supabase';
  import { useRouter } from 'vue-router';
  export default {
    setup() {
      // Get user from store
      const user = computed(() =>store.state.user);
  
      // Setup ref to router
      const router = useRouter();
  
      // Logout function
      const logout = async () => {
        await supabase.auth.signOut();
        router.push({name: 'LoginView'});
      }
  
      return {logout, user};
    },
  };
  </script>

  <style>

  </style>
  