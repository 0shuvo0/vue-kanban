<template>
    <span>
            <button @click="showModal = true" class="btn"><i class="fas fa-plus"></i> add board</button>
            <Modal
             v-if="showModal"
             title="Add Board"
             labelA="Board Title"
             labelB="Board Color"
             inputBtype="color"
             @close="showModal = false"
             @submit="handleSubmit"
            />
    </span>
</template>

<script>
import Modal from "@/components/Modal.vue"
import EventBus from "@/utils/eventBus.js"


export default {
    components: {
        Modal
    },
    data: () => ({
        showModal: false
    }),
    methods: {
        handleSubmit(data){
            EventBus.$emit("addBoard", data)
            this.showModal = false
        }
    }
}
</script>