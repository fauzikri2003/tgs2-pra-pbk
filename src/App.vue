<template>
  <div id="app">
    <h1 :style="{ color: primaryColor }">welcome to jadwal kegiatan</h1>
    <input type="text" v-model="message" placeholder="Ketik pesan di sini..." @input="updateText">
    <p :class="messageClass" :style="{ fontSize: fontSize + 'px' }">{{ message }}</p>
    <button @click="increaseFontSize">Perbesar Teks</button>
    <button @click="decreaseFontSize">Perkecilkan Teks</button>
    <button @click="toggleHighlight">Toggle Highlight</button>
    <button @click="toggleError">Toggle Error</button>
    <button @click="toggleColor">Ubah Warna Teks</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: '',
      fontSize: 16,
      isHighlighted: false,
      isError: false,
      colorChanged: false,
      primaryColor: 'black',
      originalColor: 'black',
      wallpaperIndex: 0,
    };
  },
  computed: {
    messageClass() {
      return {
        highlight: this.isHighlighted,
        error: this.isError,
        normal: !this.isError
      };
    }
  },
  methods: {
    updateText(event) {
      this.message = event.target.value;
    },
    increaseFontSize() {
      this.fontSize += 2;
    },
    decreaseFontSize() {
      this.fontSize -= 2;
    },
    toggleHighlight() {
      this.isHighlighted = !this.isHighlighted;
    },
    toggleError() {
      this.isError = !this.isError;
    },
    toggleColor() {
      this.primaryColor = this.colorChanged ? this.originalColor : 'blue';
      this.colorChanged = !this.colorChanged;
    },
    changeWallpaper() {
      this.wallpaperIndex = (this.wallpaperIndex + 1) % this.wallpapers.length;
      document.body.style.backgroundImage = this.wallpapers[this.wallpaperIndex];
      document.body.style.backgroundSize = 'cover'; // Ensure the wallpaper covers the entire background
      document.body.style.backgroundRepeat = 'no-repeat'; // Prevent the wallpaper from repeating
      document.body.style.backgroundPosition = 'center'; // Center the wallpaper
    }
  }
};
</script>

<style scoped>
.highlight {
  background-color: rgb(32, 10, 122);
}
.error {
  color: rgb(40, 11, 116);
}
.normal {
  color: rgb(237, 234, 242);
}
</style>
