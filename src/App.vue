<script setup>
import { ref } from 'vue'
import { records } from './assets/js/allRecords'

const localRecords = ref(records);
const compteur = ref(0);
function addCompteur(album) {
  album.command++;


};

function decreaseCompteur(album) {
  album.command--;


};

</script>

<template>
  <div class="min-h-screen flex flex-col">
    <header class="h-32 text-2xl w-full flex-none -ml-full shadow-lg bg-gradient-to-br from-teal-600 to-cyan-400">
      <div
        class="p-4 h-32 text-2xl w-full flex-none -ml-full rounded-2xl transform shadow-lg bg-gradient-to-br from-cyan-400 to-teal-600 -rotate-1 sm:-rotate-1">
        Disco Sciences-U (v3)</div>
    </header>


    <div class="flex flex-row ">
      <div class=" px-8 bg-cyan-100 "> <!-- left filter panel -->
        <div class="mt-2 basis-1/4">

          <div class="overflow-hidden shadow sm:rounded-md">
            <div class="bg-white p-6 w-64 h-96">

              <fieldset>
                <legend class="sr-only">Filtres</legend>
                <div class="text-base font-medium text-gray-900" aria-hidden="true">Filtres</div>
                <div class="mt-4 space-y-4">

                  <div class="flex items-start">
                    <div class="flex h-5 items-center">
                      <input id="comments" name="comments" type="checkbox"
                        class="h-4 w-4 rounded border-gray-300 text-indigo-600 focus:ring-indigo-500">
                    </div>
                    <div class="ml-3 text-sm">
                      <label for="comments" class="font-medium text-cyan-700">In stock only</label>
                    </div>

                  </div>

                </div>
                <label for="sortBy" class="block text-sm mt-2 font-medium text-cyan-700">Sort by</label>
                <select id="sortBy" name="sortBy" autocomplete="country-name"
                  class="mt-1 block w-full rounded-md border border-gray-300 bg-white py-2 px-3 shadow-sm focus:border-indigo-500 focus:outline-none focus:ring-indigo-500 sm:text-sm">
                  <option>Year </option>
                  <option>Pitchfork</option>
                </select>
              </fieldset>

            </div>

          </div>
        </div>
      </div>

      <main class="bg-white py-5 ml-6 basis-auto">
        <!-- component -->
        <section class="text-gray-600 body-font">
          <!-- one records -->
          <div class="container px-5 mx-auto" v-for="(album, index) in localRecords" :key="index">
            <div
              class="p-5 bg-white flex items-center mx-auto border-b shadow-md mb-10 border-gray-400 rounded-lg sm:flex-row flex-col">
              <div
                class="sm:w-44 sm:h-44 lg:w-40 lg:h-40 sm:mr-10 inline-flex items-center justify-center flex-shrink-0">
                <img :src="album?.coverUrl ? album.coverUrl : 'src/assets/img/default.jpg'">
              </div>
              <div class="flex-grow sm:text-left text-center mt-6 sm:mt-0">
                <h1 class="text-black text-2xl title-font font-bold mb-2">{{ album.title }}</h1>
                <h3 class="text-black text-xl title-font mb-2">{{ album.artist }}<span class="font-light mr-2">{{
                  album.year }}</span></h3>
                <p class="leading-relaxed text-base">{{ album.comment }}</p>
                <div class="py-4">


                  <div v-if="album.stock >= 1" class=" inline-block mr-2"> <!-- quand le stock est ok  -->
                    <div class="flex  pr-2 h-full items-center">
                      <svg class="text-green-500 w-6 h-6 mr-1" width="24" height="24" viewBox="0 0 24 24"
                        stroke-width="2" stroke="currentColor" fill="none" stroke-linecap="round"
                        stroke-linejoin="round">
                        <path stroke="none" d="M0 0h24v24H0z" />
                        <circle cx="12" cy="12" r="9" />
                        <path d="M9 12l2 2l4 -4" />
                      </svg>
                      <p class="title-font font-medium">{{ album.stock }} stock</p>
                    </div>
                  </div>


                  <div v-else class="inline-block mr-2"><!-- quand le stock est à zéro  -->
                    <div class="flex pr-2 h-full items-center">
                      <svg class="text-gray-500 w-6 h-6 mr-1" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                        stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                        <circle cx="12" cy="12" r="10"></circle>
                        <line x1="15" y1="9" x2="9" y2="15"></line>
                        <line x1="9" y1="9" x2="15" y2="15"></line>
                      </svg>
                      <p class="title-font font-medium">out of stock</p>
                    </div>
                  </div>
                </div>


                <div class="md:flex font-bold text-gray-800">
                  <div class="w-full md:w-1/2 flex space-x-3">
                    <div class="w-1/2">
                      <p>Pitchfork Pos: #{{ album.pitchforkPos }}</p><!-- pitchfork pos  -->
                    </div>
                  </div>
                  <div class="w-full">
                    <div class="float-right">
                      <button type="button"
                        class="border border-teal-500 bg-teal-500 text-white rounded-md px-4 py-2 m-2 ease select-none hover:bg-teal-400"
                        @click="decreaseCompteur(album)"> - </button>
                      <span>{{ album.command }}</span>
                      <button type="button"
                        class="border border-teal-500 bg-teal-500 text-white rounded-md px-4 py-2 m-2 ease select-none hover:bg-purple-800"
                        @click="addCompteur(album)"> + </button>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </section><!-- end one records -->
      </main>
    </div>
  </div>
</template>

<style scoped></style>
