<template>
    <div>
      <h1>Image Profiles</h1>
      <div v-if="imageUrls.length > 0">
        <div v-for="imageUrl in imageUrls" :key="imageUrl">
          <img :src="imageUrl" alt="Image Profile">
        </div>
      </div>
      <div v-else>
        <p>No images found</p>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  import axios from 'axios';
  
  const imageUrls = ref([]);
  
  onMounted(async () => {
    try {
      const response = await axios.get('https://testlaraveldeploy.000webhostapp.com/api/get-images'); // ปรับเป็นเส้นทางของ API ที่คุณใช้
      if (response.status === 200) {
        imageUrls.value = response.data.image_urls;
        console.log(imageUrls.value)
      } else {
        console.error('Failed to fetch image data');
      }
    } catch (error) {
      console.error('Error fetching image data', error);
    }
  });
  </script>
  