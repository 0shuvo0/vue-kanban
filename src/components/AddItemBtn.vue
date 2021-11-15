<template>
    <span>
            <button @click="showModal = true" class="btn"><i class="fas fa-plus"></i> add item</button>
            <Modal
             v-if="showModal"
             title="Add Item"
             labelA="Enter Item"
             labelB="Enter priority"
             inputBtype="text"
             @close="showModal = false"
             @submit="handleSubmit"
            />
    </span>
</template>

<script>
import Modal from "@/components/Modal.vue"
import EventBus from "@/utils/eventBus.js"


export default {
    props: ['boardId'],
    components: {
        Modal
    },
    data: () => ({
        showModal: false
    }),
    methods: {
        handleSubmit(data){
            EventBus.$emit("addItem", {
                ...data,
                boardId: this.boardId
            })
            this.showModal = false
        }
    }
}
</script>