<script setup>
import { ref } from 'vue'
import { records } from './assets/js/allRecords'
import MyHeader from './components/MyHeader.vue';
import DiscCard from './components/DiscCard.vue';
import MyFilter from './components/MyFilter.vue';


const localRecords = ref(records);

function sortByYear() {
  localRecords.value.sort((a, b) => {
    return a.year - b.year
  })

}
function sortByPos() {
  localRecords.value.sort((a, b) => {
    return a.pitchforkPos - b.pitchforkPos
  })

}
function megaSort(sort) {
  console.log(sort)
  if (sort === 'Year') sortByYear()
  else sortByPos()

}
function filterEmptyStock(bool) {
  if (bool) localRecords.value = records.filter((record) => record.stock > 0)
  else localRecords.value = records
}

function addCompteur(id) {
  // Quand on veut acceder à une ref on doit faire .value 
  const thisAlbum = localRecords.value.find((record) => record.id === id);
  if (thisAlbum.stock > 0 && thisAlbum.command < thisAlbum.stock) {
    thisAlbum.command++;
  }
};

function decreaseCompteur(id) {
  const thisAlbum = localRecords.value.find((record) => record.id === id);
  if (thisAlbum.stock > 0 && thisAlbum.command > 0) {
    thisAlbum.command--;
  }
};

function addStock(id) {
  const thisAlbum = localRecords.value.find((record) => record.id === id);
  thisAlbum.stock++;

}
function lessStock(id) {
  const thisAlbum = localRecords.value.find((record) => record.id === id);
  if (thisAlbum.stock > 0) {
    thisAlbum.stock--;
    if (thisAlbum.command > thisAlbum.stock) {
      thisAlbum.command = thisAlbum.stock;
    }
  }
}




</script>

<template>
  <div class="min-h-screen flex flex-col">
    <MyHeader />
    <div class="flex flex-row ">
      <div class=" px-8 bg-cyan-100 "> <!-- left filter panel -->
        <div class="mt-2 basis-1/4">

          <div class="overflow-hidden shadow sm:rounded-md">
            <div class="bg-white p-6 w-64 h-96">
              <MyFilter @onFilter="filterEmptyStock" @onSort="megaSort" />
            </div>

          </div>
        </div>
      </div>

      <main class="bg-white py-5 ml-6 basis-auto">
        <section class="text-gray-600 body-font">
          <DiscCard v-for="album in localRecords" :key="album.id" :TotAlbum="album" @onAdd="addCompteur"
            @onLess="decreaseCompteur" @onStockAdd="addStock" @onStockLess="lessStock" />
        </section>


      </main>
    </div>
  </div>
</template>

<style scoped></style>
