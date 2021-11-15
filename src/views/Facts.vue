<template>
    <h2>Hello {{$route.query.name}}, page {{$route.params.id}} is a {{isEven | toCap | addDot}} page</h2>
</template>

<script>
export default {
    data: () => ({
        msg: "hello"
    }),
    computed: {
        isEven(){
            return this.$route.params.id % 2 === 0 ? "even" : "odd"
        }
    },
    filters: {
        toCap(value){
            return value.toUpperCase()
        },
        addDot(value){
            return value + "."
        }
    }
}
</script>