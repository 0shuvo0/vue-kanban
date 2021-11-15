<template>
    <div>
        <h2 class="msg" v-if="boards.length == 0">You Don't Have Any Boards</h2>
        <div class="boards-container" v-else>
            <!-- <div class="board" v-for="board in boards" :key="board.title" :style="{borderColor: board.color}">
                <div class="head">
                    <span class="title">{{board.title}}</span>
                    <span class="head-btns">
                        <button class="btn"><i class="fas fa-plus"></i> add item</button>
                        <i class="fas fa-trash"></i>
                    </span>
                </div>
                <div>
                    <h2 class="msg" v-if="board.items.length == 0">No Items Yet!!!</h2>
                    <div v-else>
                        <p v-for="item in board.items" :key="item.title">
                            {{item.title}}
                        </p>
                    </div>
                </div>
            </div> -->
            <Board v-for="(board, index) in boards" :key="index" :id="index" :board="board" />
        </div>
    </div>
</template>

<script>
import Board from "@/components/Board.vue"
import EventBus from "@/utils/eventBus.js"

export default {
    components: {
        Board
    },
    mounted(){
        let temp = localStorage.getItem("boards")
        if(temp){
            this.boards = JSON.parse(temp)
        }

        EventBus.$on("addBoard", (data) => {
            this.boards.push({
                title: data.inputA,
                color: data.inputB || "#000",
                items: []
            })
        })
        EventBus.$on("addItem", (data) => {
            this.boards[data.boardId].items.push({
                title: data.inputA,
                priority: data.inputB || "low"
            })
            localStorage.setItem("boards", JSON.stringify(this.boards))
        })
        EventBus.$on("deleteBoard", (boardId) => {
            this.boards.splice(boardId, 1)
            localStorage.setItem("boards", JSON.stringify(this.boards))
        })
        EventBus.$on("deleteItem", (data) => {
            this.boards[data.boardId].items.splice(data.itemId, 1)
            localStorage.setItem("boards", JSON.stringify(this.boards))
        })
        EventBus.$on("boardSorted", () => {

            console.log(this.boards)
            localStorage.setItem("boards", JSON.stringify(this.boards))
        })
    },
    data: () => ({
        boards: []
    }),
    watch: {
        boards(){
            localStorage.setItem("boards", JSON.stringify(this.boards))
            console.log("boards changed")
        }
    }
}
</script>