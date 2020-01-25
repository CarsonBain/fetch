<template>
  <div class="w-full bg-indigo-100 py-5">
    <div class="max-w-4xl mx-auto px-10 flex items-center">
      <a href="/" class="flex items-center">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          height="24px"
          width="24px"
          class="mr-2"
          viewBox="0 0 512 512"
        >
          <path
            d="M442 185.5v-140H263.082a60.001 60.001 0 00-53.666 33.167L176 145.5H0v30l62.725 109.768A60.002 60.002 0 00114.82 315.5H246v151h266v-211l-70-70z"
            fill="#fedbab"
          />
          <path
            d="M512 255.5l-70-70v-140H263.082a60.001 60.001 0 00-53.666 33.167L176 145.5l203 261v60h133v-211z"
            fill="#fec478"
          />
          <path
            d="M382 195.5c-33.137 0-60-26.863-60-60v-90h120v90c0 33.137-26.863 60-60 60z"
            fill="#e08344"
          />
          <circle cx="246" cy="140.5" r="20" fill="#713708" />
          <path fill="#00c3ff" d="M246 406.5h266v60H246z" />
          <path fill="#00aaf0" d="M379 406.5h133v60H379z" />
          <path fill="#713708" d="M0 145.5v30l9.532 16.681L56.213 145.5z" />
        </svg>
        <h1 class="text-2xl text-gray-800 font-display">
          {{ title }}
        </h1>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Nav',
  data() {
    return {};
  },
  props: {
    title: String
  }
};
</script>

<style scoped></style>
