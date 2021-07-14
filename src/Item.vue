<template>
    <div class="warp">
    <div v-for="(a,i) in oneroom" :key="i" class="card_box">
        <img :src="a.image" alt="" class="room-img">
        <h4 class="red" style="color:red" @click="$emit('openModal',a.id)">{{ a.title }}</h4>
        <p>{{ a.price }} 만원</p>
    </div>
    </div>
</template>

<script>
export default {
    name : 'Item',
    props: {
        oneroom: Array
    },
    methods: {
        send(){
            this.$emit('openModal',this.oneroom.id)
        }
    },
}
</script>

<style>
    
</style>