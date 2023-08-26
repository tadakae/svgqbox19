<template>
<!--    <div class="icons">-->
<!--        <div class="all_style">-->
<!--            <b>All Style</b>-->
<!--            <div class="border_div"></div>-->
<!--        </div>-->
    <div class="input_big">
        <input @input="searchInput"
               class="gig-input" type="search"  placeholder="search" v-model="search">
    </div>



        <div class="icon_box">
            <div class="icons_main" v-for="(icon, key) in filteredIcons" :key="key"  >
                <img :src="icon.url" style="width: 45px; margin: 20px; " alt="">
            </div>
        </div>

<!--    </div>-->
</template>

<script>

import axios from "axios";

export default {
    name: "All_Icons",
    data() {
        return {
            icons: [],
            search:''
        }
    },
    methods: {
        async getIcons() {
            const { data } = await axios.get("https://svg.q19.kz/api/v1/icons/", {
                params: {
                    limit: 60,
                    keyword: this.search,

                }
            })
            console.log("res", data)
            this.icons = data.data

        },
        searchInput(event) {


            return this.icons.filter(elem => {
                return elem.keywords.includes(this.search)

            })

        },




    },



    computed: {
        filteredIcons() {
            this.getIcons()
            return this.icons
        }
    },

    mounted() {
        this.getIcons();
    },

}
</script>

<style scoped>

.icons {
    margin-top: 50px;
    margin-left: 80px;
    width: 1280px;
    height: 635px;
    background-color: white;
    border-radius: 20px;
    margin-bottom: 450px;

}

.all_style {
    padding-top: 35px;
    margin-left: 40px;
    font-weight: 100;
}

.border_div {
    width: 1200px;
    height: 2px;
    background-color: #f2f2f2;
    margin-top: 10px;
}

.icon_box {
    width: 1200px;
    height: max-content;
    border: none;
    margin-top: 20px;
    border-radius: 12px;
    display: flex;
    flex-wrap: wrap;
    margin-left: 120px;
    margin-bottom: 150px;
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