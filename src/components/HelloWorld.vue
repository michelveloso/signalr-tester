<script setup>
defineProps({
  msg: {
    type: String,
    required: true
  },
  url: {
    type: String,
    required: true,
    default: null
  },
  error: {
    type: String,
    required: true,
    default: null
  }  
})
</script>

<template>
  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
    <h3 v-if="url">
      WebSocket URL: <span style="font-weight: bold;">{{ url }}</span>
    </h3>
    <h3 v-if="error" style="padding-top: 10px;">
      <span style="font-weight: bold; color: brown;">{{ error }}</span>
    </h3>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
