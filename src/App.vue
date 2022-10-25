<script>
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      showOrHideComponentName: false,
      // home / animes / contactMe
      whichContent: "home",
      stateData: "",
      formInputData: "",
      topAnimes: [],
    };
  },
  methods: {
    formSubmissionOnClickHandler() {
      this.stateData = this.formInputData;
    },
    async fetchDataFromJikan() {
      try {
        const { data } = await axios.get(`https://api.jikan.moe/v4/top/anime`);
        this.topAnimes = data.data
          .map((anime) => ({
            title: anime.title,
            imageUrl: anime.images?.jpg?.image_url,
            totalEpisodes: anime.episodes,
            status: anime.status,
          }))
          .slice(1, 4);
      } catch (err) {
        console.log(err);
      }
    },
  },
  created() {
    this.fetchDataFromJikan();
  },
};
</script>

<template>
  <div class="p-2 flex flex-col gap-2 text-slate-700">
    <!-- NavBar -->
    <section
      class="p-4"
      v-bind:class="showOrHideComponentName ? 'border-2 border-slate-200' : ''"
    >
      <h1
        class="text-xl"
        v-bind:class="showOrHideComponentName ? '' : 'hidden'"
      >
        Component NavBar
      </h1>

      <nav class="flex gap-2 justify-between bg-gray-200 py-4 px-4 rounded-xl">
        <div class="my-auto">Brand Logo</div>

        <div class="flex gap-2">
          <a
            href="#"
            class="my-auto hover:text-blue-600 hover:underline"
            v-on:click.prevent="
              () => {
                whichContent = 'home';
              }
            "
            >Home</a
          >
          <a
            href="#"
            class="my-auto hover:text-blue-600 hover:underline"
            v-on:click.prevent="
              () => {
                whichContent = 'animes';
              }
            "
            >Animes</a
          >
          <a
            href="#"
            class="my-auto hover:text-blue-600 hover:underline"
            v-on:click.prevent="
              () => {
                whichContent = 'contactMe';
              }
            "
            >Contact Me</a
          >
        </div>

        <div class="flex gap-2">
          <div>
            <svg
              width="32"
              height="32"
              viewBox="0 0 24 24"
              class="text-slate-600"
            >
              <path
                fill="currentColor"
                d="M15.5 14h-.79l-.28-.27A6.471 6.471 0 0 0 16 9.5A6.5 6.5 0 1 0 9.5 16c1.61 0 3.09-.59 4.23-1.57l.27.28v.79l5 4.99L20.49 19l-4.99-5zm-6 0C7.01 14 5 11.99 5 9.5S7.01 5 9.5 5S14 7.01 14 9.5S11.99 14 9.5 14z"
              />
            </svg>
          </div>

          <div>
            <svg
              width="32"
              height="32"
              viewBox="0 0 24 24"
              class="text-slate-600"
            >
              <path
                fill="currentColor"
                d="m17 8l-1.41 1.41L17.17 11H9v2h8.17l-1.58 1.58L17 16l4-4l-4-4zM5 5h7V3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h7v-2H5V5z"
              />
            </svg>
          </div>
        </div>
      </nav>
    </section>

    <!-- Content -->
    <section
      class="p-4"
      v-bind:class="showOrHideComponentName ? 'border-2 border-red-100' : ''"
    >
      <h1
        class="text-xl"
        v-bind:class="showOrHideComponentName ? '' : 'hidden'"
      >
        Component Content
      </h1>

      <!-- Content Home -->
      <div
        class="p-4 bg-gray-200 rounded-xl flex gap-2 flex-col"
        v-if="whichContent === 'home'"
      >
        <h3 class="text-base">Ini adalah bagian konten (Home)</h3>
      </div>

      <!-- Content Animes -->
      <div
        class="p-4 bg-gray-200 rounded-xl flex gap-2 flex-col"
        v-if="whichContent === 'animes'"
      >
        <h3 class="text-base">Ini adalah bagian konten (Animes)</h3>

        <section
          class="p-4"
          v-bind:class="
            showOrHideComponentName ? 'border-2 border-red-400' : ''
          "
        >
          <h1
            class="text-xl"
            v-bind:class="showOrHideComponentName ? '' : 'hidden'"
          >
            Component Table Animes
          </h1>

          <!-- Table Animes -->
          <table
            class="mx-auto table-auto border border-spacing-2 border-separate border-red-300"
          >
            <thead>
              <tr>
                <th class="border border-red-300">#</th>
                <th class="border border-red-300">Thumbnail</th>
                <th class="border border-red-300">Title</th>
                <th class="border border-red-300">Episodes</th>
                <th class="border border-red-300">Status Airing</th>
              </tr>
            </thead>
            <tbody>
              <template v-for="(anime, idx) in topAnimes" :key="'anime' + idx">
                <tr v-bind:class="showOrHideComponentName ? '' : 'hidden'">
                  <td colspan="5" class="text-xl">
                    <p>Component Table Animes Row</p>
                  </td>
                </tr>
                <tr>
                  <td class="border border-red-300">{{ idx + 1 }}</td>
                  <td class="border border-red-300">
                    <img :src="anime.imageUrl" class="w-16 h-24" />
                  </td>
                  <td class="border border-red-300">{{ anime.title }}</td>
                  <td class="border border-red-300">
                    {{ anime.totalEpisodes }}
                  </td>
                  <td class="border border-red-300">{{ anime.status }}</td>
                </tr>
              </template>
            </tbody>
          </table>
        </section>
      </div>

      <!-- Content Contact -->
      <div
        class="p-4 bg-gray-200 rounded-xl flex gap-2 flex-col"
        v-if="whichContent === 'contactMe'"
      >
        <h3 class="text-base">Ini adalah bagian konten (Contact Me)</h3>

        <!-- Form Input -->
        <section
          class="p-4"
          v-bind:class="
            showOrHideComponentName ? 'border-2 border-red-400' : ''
          "
        >
          <h1
            class="text-xl"
            v-bind:class="showOrHideComponentName ? '' : 'hidden'"
          >
            Component Form Input
          </h1>

          <form
            class="my-2 flex flex-col gap-2"
            v-on:submit.prevent="formSubmissionOnClickHandler"
          >
            <input
              type="text"
              class="py-4 px-2 rounded-xl"
              placeholder="Inputan dari Form"
              v-model="formInputData"
            />
            <button
              type="submit"
              class="bg-blue-200 hover:bg-blue-400 mx-auto mt-4 p-4 rounded-full w-full"
            >
              Kirimin Yuk !
            </button>
          </form>
        </section>

        <!-- Form Result -->
        <section
          class="p-4"
          v-bind:class="
            showOrHideComponentName ? 'border-2 border-red-400' : ''
          "
        >
          <h1
            class="text-xl"
            v-bind:class="showOrHideComponentName ? '' : 'hidden'"
          >
            Component Form Result
          </h1>

          <div class="p-4 my-2 bg-green-200 rounded-xl">
            Tulisan dari Form adalah:
            {{ stateData ? stateData : "Empty Placeholder" }}
          </div>
        </section>
      </div>
    </section>

    <!-- Footer -->
    <section
      class="p-4"
      v-bind:class="showOrHideComponentName ? 'border-2 border-green-200' : ''"
    >
      <h1
        class="text-xl"
        v-bind:class="showOrHideComponentName ? '' : 'hidden'"
      >
        Component Footer
      </h1>

      <div class="p-4 bg-gray-200 rounded-xl">
        <h3 class="text-base text-center">
          &copy;&nbsp;withered-flowers - 2022
        </h3>
      </div>
    </section>

    <!-- Toggle Button -->
    <section class="mx-auto mt-4">
      <button
        class="p-4 rounded-full w-96"
        v-bind:class="
          showOrHideComponentName
            ? 'bg-blue-200 hover:bg-blue-400'
            : 'bg-red-200 hover:bg-red-400'
        "
        v-on:click="
          () => {
            showOrHideComponentName = !showOrHideComponentName;
          }
        "
      >
        {{ !showOrHideComponentName ? "Show Component" : "Hide Component" }}
      </button>
    </section>
  </div>
</template>

<style scoped></style>
