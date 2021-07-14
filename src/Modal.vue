<template>
    <div class="black-bg" v-if="모달창열렸니">
        <div class="white-bg" >
            <img :src="oneroom[데이터정보].image" alt="">
            <h4>{{oneroom[데이터정보].title}}</h4>
            <p>{{oneroom[데이터정보].content}}</p>
            <!-- <input type="number" :value="month" @input="month = $event.target.value"> -->
            <!-- <input v-model.number="month" type="range" min="1" max="12"><br> -->
            <input v-model.number="month"><br>
            <!-- 여기서 넘버는 받은 데이터를 넘버로 바꿔주세요 일뿐, 막아주지는 못함 -->
            <!-- <select v-model="month">
                <option v-for="(a,i) in 12" :key="i" :value="a" >{{a}}개월</option>
            </select> -->

            <!-- watcher : 데이터 감시할때 쓰는 함수 -->
            <p>{{month}}개월 선택함 / {{oneroom[데이터정보].price * month}}  원</p>
            <br>
            <button class="modal_close" @click="$emit('closeModal')">닫기</button>
        </div>
    </div>
</template>

<script>
export default {
    name : 'Madal',
    data(){
        return{
            month : 1,
        }
    },
    // 업데이트되기전에(렌더링되기전에 막아버리기)
    beforeUpdate() {
        if(this.month==2){
            alert('우리는 2개월은 안해영');
            this.month=10
        }
    },
    watch:{
        //파라미터 왼쪽은 변경 후 데이터, 오른쪽은 변경 전 데이터
        month(a,b){ //month가 변경될떄마다 watcher 실행됨
            // 사용자가 month를 글자로 입력하면 경고문 띄워주셈
            if(isNaN(a)==true){
                alert('문자입력마셈');
                this.month = 1;
            }
            if(a>12){
                alert('13이상 입력하지 마셈');
                this.month = 1;
                b;
            }
            // }else if(a==2){
            //     alert('우리는 2개월은 안해영');
            //     this.month = b;
            // }else if(a==0){
            //     alert('0이상의 숫자를 입려해주세용');
            //     this.month = b;
            // }
        },
    },
    methods: {
        
    },
    props: {
        oneroom: Array,
        모달창열렸니 : Boolean,
        데이터정보 : Number
    }
    
}
</script>

<style>
    
</style>