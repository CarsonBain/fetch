<template>
  <div class="mx-auto max-w-xl h-full px-16 py-16">
    <div class="image-wrap relative">
      <transition name="fade">
        <div
          v-if="!isLoaded"
          class="h-full w-full absolute flex content-center items-center flex-col"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            height="100px"
            width="100px"
            viewBox="0 0 512.002 512.002"
          >
            <path
              d="M176.093 376.7V275.836h-53.028c-17.843-.022-34.447-9.713-43.349-25.292l-38.694-67.777v-36.999h99.877l15.546-30.386c8.557-17.054 25.719-27.645 44.805-27.645h110.914v90.835l58.436 58.436-73.444 114.179L176.093 376.7z"
              fill="#fedbab"
            />
            <path
              d="M312.164 178.572V87.737H201.25c-19.086 0-36.247 10.59-44.805 27.645l-15.546 30.386L316.4 321.269l54.199-84.261-58.435-58.436z"
              fill="#fec478"
            />
            <path
              d="M195.103 390.207C87.523 390.207 0 302.684 0 195.104S87.523.002 195.103.002s195.103 87.523 195.103 195.103-87.524 195.102-195.103 195.102zm0-360.189c-91.029 0-165.087 74.058-165.087 165.087s74.058 165.087 165.087 165.087S360.19 286.134 360.19 195.105 286.131 30.018 195.103 30.018z"
              fill="#0a4eaf"
            />
            <path
              fill="#032e68"
              d="M490.777 512.005l-178.94-178.94 21.224-21.223 178.94 178.94z"
            />
            <path
              d="M262.138 207.8c-27.584 0-50.026-22.442-50.026-50.026V87.737h100.053v70.037c-.001 27.584-22.443 50.026-50.027 50.026z"
              fill="#e08344"
            />
            <path fill="#713708" d="M41.022 145.768v36.999l40.021-36.999z" />
            <path
              d="M195.103.002v30.016c91.029 0 165.087 74.058 165.087 165.087s-74.058 165.087-165.087 165.087v30.016c107.58 0 195.103-87.523 195.103-195.103S302.682.002 195.103.002z"
              fill="#063e8b"
            />
          </svg>
          <p class="text-lg">Fetching...</p>
        </div>
      </transition>
      <img
        v-if="isLoaded"
        :src="image"
        alt=""
        class="max-h-full max-w-full mx-auto"
      />
    </div>
    <div class="mt-6 mx-auto w-64">
      <label
        for="breeds"
        class="text-xs uppercase text-gray-600 tracking-wider font-semibold mb-1 block"
        >Breeds</label
      >
      <div class="relative">
        <select
          name="breeds"
          v-model="selectedBreed"
          @change="getData(selectedBreed)"
          class="block appearance-none w-full bg-gray-200 px-4 py-2 pr-8 rounded leading-tight focus:outline-none focus:shadow-outline"
        >
          <option v-for="(breed, i) in breeds" :value="breed" :key="i">
            {{ breed.charAt(0).toUpperCase() + breed.slice(1) }}
          </option>
        </select>
        <div
          class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-gray-700"
        >
          <svg
            class="fill-current h-4 w-4"
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 20 20"
          >
            <path
              d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"
            />
          </svg>
        </div>
      </div>
      <h2 class="text-xs mt-2 mb-6 text-gray-600">
        Select a breed or fetch a random pooch and enjoy :')
      </h2>
    </div>
    <button
      @click="getData(selectedBreed)"
      class="my-4 block px-10 py-3 bg-indigo-600 text-white rounded mx-auto text-sm w-64"
    >
      Another please
    </button>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Dogs',
  data() {
    return {
      random: {},
      isLoaded: false,
      error: '',
      breeds: [],
      selectedBreed: 'random'
    };
  },
  computed: {
    image: function() {
      return this.random.message;
    }
  },
  created() {
    axios.get('https://dog.ceo/api/breeds/list/all').then(response => {
      this.breeds = ['random', ...Object.keys(response.data.message)];
    });
  },
  methods: {
    getData: function(selected = 'random') {
      let apiUrl = '';

      if (selected === 'random') {
        apiUrl = 'https://dog.ceo/api/breeds/image/random';
      } else {
        apiUrl = `https://dog.ceo/api/breed/${selected}/images/random`;
      }
      axios
        .get(apiUrl)
        .then(response => {
          this.random = response.data;
          this.isLoaded = true;
        })
        .catch(error => {
          this.error = error.response;
          this.isLoaded = false;
        });
    },
    getBreeds: function() {
      axios.get('https://dog.ceo/api/breeds/list/all').then(response => {
        this.breeds = response.data.message;
      });
    }
  },
  mounted() {
    this.getData();
  }
};
</script>

<style scoped>
.image-wrap {
  height: 225px;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
