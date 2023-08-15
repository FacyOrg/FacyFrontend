<template>
<div class="fancy-upload">
    <form @submit.prevent="uploadImage">
      <label class="custom-file-upload">
        <input type="file" accept="image/*" @change="handleFileChange">
        <span>Select an Image</span>
      </label>
      <button type="submit" class="upload-button">Upload Image</button>
    </form>

    <div v-if="imageUplaoded">
      <img :src="imageURL" alt="Uploaded Image" class="uploaded-image" />
    </div>
  </div>
</template>

<script lang="ts">
export default {
  data() {
    return {
      selectedFile: null,
      imageUplaoded: false,
      imageURL: ''
    };
  },
  methods: {
    handleFileChange(event: any) {
      this.selectedFile = event.target.files[0];
    },
    async uploadImage() {
      if (this.selectedFile) {
        const formData = new FormData();
        formData.append('image', this.selectedFile);
        // try {
        //   const response = await fetch('', {
        //     method: 'POST',
        //     body: formData,
        //   });
        //   if (response.ok) {
        //     console.log("Image uploaded successfully");
        //   }
        //   else {
        //     console.log("Image upload failed");
        //   }
        // } catch (error) {
        //   console.log("Error uploading image: " ,error);
        // }
        console.log(this.selectedFile);
        this.imageURL = URL.createObjectURL(this.selectedFile);
        this.imageUplaoded = true;
      }
    },
  },
};
</script>

<style scoped>
.fancy-upload {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
}

.custom-file-upload {
  display: inline-block;
  background-color: turquoise;
  border: 1px solid #ddd;
  border-radius: 4px;
  padding: 6px 12px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.custom-file-upload:hover {
  background-color: #e0e0e0;
}

.custom-file-upload input[type="file"] {
  display: none;
}

.upload-button {
  margin-top: 10px;
  padding: 10px 20px;
  background-color: #007bff;
  border: none;
  border-radius: 4px;
  color: white;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.upload-button:hover {
  background-color: #0056b3;
}

.uploaded-image {
  margin-top: 20px;
  max-width: 50%;
  height: auto;
  display: block;
  margin: 20px auto;
}
</style>
