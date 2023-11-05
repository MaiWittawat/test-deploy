
<template>
    this is index page
    <div v-if="data">
        <div v-for="user in data">
            {{ user }}
        </div>
    </div>
  
    <nuxt-link to="/profile">go to profile</nuxt-link>
  </template>
  
  <script setup>
  
  
  const data = ref();
  const time = ref();
  
  const getAll = async () => {
    const { data: res, error } = useFetch("https://testlaraveldeploy.000webhostapp.com/api/AllUser");
  
    if (res.value !== null) {
      data.value = res.value
      console.log(data.value)
    }
  };
  
  getAll();
  </script>
  