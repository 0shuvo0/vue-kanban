<template>
    <div class="item">
        <div class="head">
            <span class="priority">
                <span>Priority:</span>
                <span class="badge" :style="{backgroundColor: priorityClr}">{{item.priority}}</span>
            </span>
            <i class="fas fa-sort handle" :style="{color: clr}"></i>
        </div>
        <p class="title">{{item.title}}</p>
        <p class="text-right">
            <button class="btn delete" @click="handleItemDelete">delete</button>
        </p>
    </div>
</template>

<script>
import EventBus from "@/utils/eventBus.js"

export default {
    props: ['item', 'clr', 'boardId', 'itemId'],
    computed: {
        priorityClr(){
            if(this.item.priority == 'low'){
                return '#d0c6fc';
            } else if(this.item.priority == 'medium'){
                return '#80d5db';
            } else if(this.item.priority == 'high'){
                return '#d13667';
            }
        }
    },
    methods: {
        handleItemDelete(){
            EventBus.$emit('deleteItem', {
                boardId: this.boardId,
                itemId: this.itemId
            });
        }
    }
}
</script>