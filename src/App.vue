<template>
  <div id="app" class="flex-col min-h-full">
    <div class="h-full text-center">
      <div class="text-6xl text-purple-600">
        Whiskers R We
      </div>
      <div class="text-base">
        We now do curbside delivery! Order one cat and we'll leave 10 to 15 on
        your porch.
      </div>
      <div class="text-xs">
        By Barbara DeDrew
      </div>
    </div>
    <div class="p-4 grid grid-cols-3 grid-rows-3 gap-4">
      <div
        class="text-left border border-purple-600 border-solid"
        v-for="(catPicture, index) of catPictures"
        :key="catPicture"
      >
        <div class="flex flex-col h-full">
          <div class="self-center text-4xl text-pink-500">
            {{ catNames[index] }}
            <div v-show="adopted[index]" class="text-green-500">
              Adopted!
            </div>
          </div>
          <div class="self-center h-full">
            <img :src="catPicture" height="50" />
          </div>
          <div class="self-end h-full mt-2 mb-2 mr-2 align-bottom">
            <button
              class="p-2 text-white bg-green-500 border border-black border-solid rounded hover:bg-pink-500 confetti-button"
              @click="adoptMe(index)"
            >
              Adopt me!
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      catPictures: [],
      catNames: [
        "Mr. Frisky",
        "Bubbles",
        "Baxter",
        "Marbles",
        "Boots",
        "Spenser",
        "Shanghai",
        "Judi Dench",
        "Bandit",
      ],
      adopted: [],
    };
  },
  methods: {
    adoptMe(index) {
      this.adopted[index] = true;
    },
  },
  async mounted() {
    const response = await fetch(
      "https://api.thecatapi.com/v1/images/search?size=small&limit=9",
      {
        method: "GET",
        headers: {
          "x-api-key": "95435c03-a4d8-4b69-8d67-5e2e621eaa82",
        },
      },
    );
    let catData = await response.json();
    for (const cat of catData) {
      this.catPictures.push(cat.url);
    }
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-top: 60px;
}
</style>
