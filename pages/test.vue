<template>
    <div>
      <form @submit.prevent="uploadImage">
        <input type="file" ref="fileInput"  @change="handleFileChange" accept="image/*" multiple>
        <button type="submit">Upload</button>
      </form>
      <div v-if="uploadedImageUrl">Uploaded Image:</div>
      <!-- <img v-if="uploadedImageUrl" :src="uploadedImageUrl" alt="Uploaded Image"> -->
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const fileInput = ref(null);
  const uploadedImage = ref(null);
  // const uploadedImageUrl = ref(null);
  
  // const handleFileChange = () => {
  //   uploadedImage.value = fileInput.value.files[0];
  // };
  
  // const uploadImage = async () => {
  //   if (uploadedImage.value) {
  //     const formData = new FormData();
  //     formData.append('image', uploadedImage.value);
  
  //     try {
  //       const response = await fetch('http://localhost/api/upload-image', {
  //         method: 'POST',
  //         body: formData,
  //       });
  
  //       if (response.ok) {
  //         const data = await response.json();
  //         if (data.image_url) {
  //           uploadedImageUrl.value = data.image_url;
  //         } else {
  //           console.error('No image URL in response');
  //         }
  //       } else {
  //         console.error('Failed to upload image');
  //       }
  //     } catch (error) {
  //       console.error('Error uploading image:', error);
  //     }
  //   }
  // };
  
  
  const handleFileChange = () => {
    // Clear any previously selected files
    uploadedImage.value = null;
    // Set uploadedImage to an array of selected files
    uploadedImage.value = Array.from(fileInput.value.files);
  };
  
  const uploadImage = async () => {
    if (uploadedImage.value.length > 0) {
      const formData = new FormData();
  
      // Append each selected file to the FormData
      uploadedImage.value.forEach((file, index) => {
        formData.append(`image[${index}]`, file);
      });
  
      try {
        const response = await fetch('https://testlaraveldeploy.000webhostapp.com/api/upload-image', {
          method: 'POST',
          body: formData,
        });
  
        if (response.ok) {
          console.log("ok")
          console.log(response)
  
        } else {
          console.error('Failed to upload image');
        }
      } catch (error) {
        console.error('Error uploading image:', error);
      }
    }
  };
  
  </script>
  