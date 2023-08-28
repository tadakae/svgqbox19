<template>
    <div class="input_big">
        <input @keypress.enter="searchInput"
               id="myInput"
               class="gig-input"
               type="search"
               placeholder="search"
               v-model="search">
    </div>

    <div class="icon_box">
        <div class="icons_main" v-for="icon in icons" :key="icon.id">
            <img :src="icon.url" style="width: 45px; margin: 20px; " alt="">
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

}


</style>