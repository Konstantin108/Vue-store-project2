<template>
    <form action="#"
          class="search-form"
          @submit.prevent="$parent.$refs.products.filter(userSearch)">
        <input type="text" class="text_search" v-model="userSearch" placeholder="Search for item...">
        <button class="search_button" type="submit">
            <img src="img/search_image.png" alt="search_image">
        </button>
    </form>
</template>

<script>
    export default {
        name: 'filter-el',
        data() {
            return {
                userSearch: '',
            };
        },
    }
</script>
