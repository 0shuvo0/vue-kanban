<template>
    <div>
        <img :src="errorImg" alt="">
        <p class="text-center">
            <router-link to="/">Go to Home</router-link>
        </p>
    </div>
</template>

<script>
import errorImg from "@/assets/error.svg"
export default {
    data: () => ({
        errorImg
    })
}
</script>