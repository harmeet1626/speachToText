<!-- SpeechToText.vue -->

<template>
  <div>
    <button @click="startSpeechRecognition">Start Speech Recognition</button>
    <div v-if="transcription">Transcription: {{ transcription }}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      transcription: '',
    };
  },
  methods: {
    startSpeechRecognition() {
      const recognition = new webkitSpeechRecognition() || new SpeechRecognition();

      recognition.lang = 'en-US';

      recognition.onresult = (event) => {
        const result = event.results[event.results.length - 1][0].transcript;
        this.transcription = result;
      };

      recognition.onerror = (event) => {
        console.error('Speech recognition error:', event.error);
      };

      recognition.onend = () => {
        console.log('Speech recognition ended.');
      };

      recognition.start();
    },
  },
};
</script>

<style scoped>
/* Add your component styles here */
</style>
