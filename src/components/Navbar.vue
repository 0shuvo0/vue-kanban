<template>
    <div class="navbar container">
        <!-- <a href="#" class="logo">Vue-KanBan</a> -->
        <router-link to="/" class="logo">Vue-KanBan</router-link>
        <div class="nav-links">
            <router-link v-for="(link, index) in links" :class="{active: link.path == $route.path}" :key="index" :to="link.path">{{link.name}}</router-link>
            <AddBoardBtn />
        </div>
    </div>
</template>

<script>
import AddBoardBtn from "@/components/AddBoardBtn.vue"

export default {
    components: {
        AddBoardBtn
    },
    data: () => ({
        links: [
            {
                name: 'home',
                path: '/'
            },
            {
                name: 'facts',
                path: '/facts/20'
            },
            {
                name: 'about',
                path: '/about'
            }
        ]
    })
}
</script>