<template>
    <div class="input_big">
        <input @keypress.enter="searchInput"
               id="myInput"
               class="gig-input"
               type="search"
               placeholder="search"
               v-model="search">
        <div class="search_svg">
            <svg width="25px" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" transform="rotate(0)"><g id="SVGRepo_bgCarrier" stroke-width="0"></g><g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g><g id="SVGRepo_iconCarrier"> <path d="M20 20L15.8033 15.8033C15.8033 15.8033 14 18 10.5 18C6.35786 18 3 14.6421 3 10.5C3 6.35786 6.35786 3 10.5 3C14.6421 3 18 6.35786 18 10.5C18 11.0137 17.9484 11.5153 17.85 12" stroke="#ffffff" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"></path> </g></svg>
        </div>
    </div>


    <div class="icon_box">
        <div class="icons_main" v-for="icon in icons" :key="icon.id">
            <img :src="icon.url" style="width: 45px; margin: 20px; " alt="" >
        </div>
    </div>
    <Pagination />








</template>

<script>

import axios from "axios";
import Pagination from "@/components/Pagination.vue";


export default {
    name: "All_Icons",
    components: {Pagination},

    data() {

        return {
            icons: [],
            search: ''
        }

    },
    methods: {

        async getIcons() {
            const {data} = await axios.get("https://svg.q19.kz/api/v1/icons/", {
                params: {
                    limit: 60,
                    keyword: this.search.toLowerCase(),
                    page: 1

                }
            })
            console.log("res", data)
            this.icons = data.data
        },


         searchInput(event) {
             this.filteredIcons();
         },
        filteredIcons() {
                     this.getIcons()
                    return this.icons
                }
    },




    created() {
        this.getIcons()
    },


}
</script>

<style scoped>


.icon_box {
    width: 1200px;
    height: max-content;
    border: none;
    margin-top: 20px;
    border-radius: 12px;
    display: flex;
    flex-wrap: wrap;
    margin-left: 120px;

}

.icons_main {
    background-color: snow;
    border: 3px solid darkgray;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100px;
    height: 100px;
    margin: 10px;
    border-radius: 15px;
    z-index: 99;
    cursor: pointer;

}

.search_svg {
    position: absolute;
    margin-left: 125px;
    margin-top: -5px;
}


</style>