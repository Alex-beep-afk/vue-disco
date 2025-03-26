<script setup>
import { ref } from 'vue';

const emit = defineEmits(['onFilter', 'onSort']);

function onFilter() {
    emit('onFilter', checkboxValue.value);
}

function onSort() {

    emit('onSort', sortBy.value);
}

const checkboxValue = ref(false);
const sortBy = ref('');

</script>
<template>
    <fieldset>
        <legend class="sr-only">Filtres</legend>
        <div class="text-base font-medium text-gray-900" aria-hidden="true">Filtres</div>
        <div class="mt-4 space-y-4">

            <div class="flex items-start">
                <div class="flex h-5 items-center">
                    <input v-model="checkboxValue" @change="onFilter" id="comments" name="comments" type="checkbox"
                        class="h-4 w-4 rounded border-gray-300 text-indigo-600 focus:ring-indigo-500">
                </div>
                <div class="ml-3 text-sm">
                    <label for="comments" class="font-medium text-cyan-700">In stock only</label>
                </div>
            </div>

        </div>
        <label for="sortBy" class="block text-sm mt-2 font-medium text-cyan-700">Sort by</label>
        <select v-model="sortBy" @change="onSort" id="sortBy" name="sortBy" autocomplete="country-name"
            class="mt-1 block w-full rounded-md border border-gray-300 bg-white py-2 px-3 shadow-sm focus:border-indigo-500 focus:outline-none focus:ring-indigo-500 sm:text-sm">
            <option>Year </option>
            <option>Pitchfork</option>
        </select>
    </fieldset>

</template>
<style scoped></style>