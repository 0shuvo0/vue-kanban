<template>
    <div class="board" :style="{borderColor: board.color}">
        <div class="head">
            <span class="title">{{board.title}}</span>
            <span class="head-btns">
                <!-- <button class="btn"><i class="fas fa-plus"></i> add item</button> -->
                <AddItemBtn :boardId="id" />
                <i class="fas fa-trash" @click="handleBoardDelete"></i>
            </span>
        </div>
        <div>
            <h2 class="msg" v-if="board.items.length == 0">No Items Yet!!!</h2>
            <div v-else>
                <draggable v-model="board.items" group="items" handle=".handle" @sort="handleSort">
                    <transition-group name="list">
                        <Item  v-for="(item, index) in board.items" :key="item.title" :item="item" :boardId="id" :itemId="index" :clr="board.color" />
                    </transition-group>
                </draggable>
            </div>
        </div>
    </div>
</template>

<script>
import draggable from 'vuedraggable'

import Item from "@/components/Item.vue"
import AddItemBtn from "@/components/AddItemBtn.vue"
import EventBus from "@/utils/eventBus.js"

export default {
    components: {
        Item,
        AddItemBtn,
        draggable
    },
    props: {
        board: {
            required: true,
            type: Object
        },
        id: {
            required: true,
            type: Number
        }
    },
    methods: {
        handleBoardDelete() {
            EventBus.$emit("deleteBoard", this.id)
        },
        handleSort(){
            EventBus.$emit("boardSorted")
        }
    }
}
</script>