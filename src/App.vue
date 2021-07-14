<template>

<!-- <div class="start" :class="{end : 모달창열렸니}">
  <Modal :oneroom="oneroom" :모달창열렸니="모달창열렸니" :데이터정보="데이터정보" @closeModal="모달창열렸니 = false"></Modal>
</div> -->

<transition name="fade">
  <Modal :oneroom="oneroom" :모달창열렸니="모달창열렸니" :데이터정보="데이터정보" @closeModal="모달창열렸니 = false"></Modal>
</transition>
  



<div class="menu">
  <a v-for="(a,i) in 메뉴들" :key="i"> {{a}} </a>
</div>

<Discount :discountRate="할" v-if="showDiscount == true"></Discount>

<button @click="priceSort()">가격낮은순정렬</button>
<button @click="priceSortHigh()">가격높은순정렬</button>
<button @click="sortBack()">되돌리기</button>

<Item :oneroom="oneroom" @openModal="모달창열렸니 = true; 데이터정보 = $event"></Item>


</template>

<script>

import data from './assets/oneroom.js';
import Discount from './Discount.vue';
import Modal from './Modal.vue';
import Item from './Item.vue';

// ui의 현재 상태를 데이터로 저장해둠



export default {
  name: 'App',
  data(){
    return {
      할 : 30,
      showDiscount : true,
      오브젝트 : {name :'kim', age:20},
      데이터정보 : 0,
      모달창열렸니 : false,
      메뉴들 : ['Home','Shop','About'],
      oneroomOriginal : [...data],
      oneroom :  data
      // array/object데이터의 각각 별개의 사본을 만들려면 [...array자료]
    }
  },
  methods: {
    increase(i){
      console.log(i);
    },
    priceSort(){
      /* 
      var array = [3,5,2];
      array.sort(function(a,b){
        return a - b;
        // 여기서 a,b는 각 3과 5 (첫실행되었을때)
        // 리턴 값이 마이너스면 a를 왼쪽으로 ~
        // 리턴 값이 플러스면 a를 오른쪽으로 ~
      })
      */
      this.oneroom.sort(function(a,b){
        return a.price - b.price;
      })
    },
    sortBack(){
      // this.oneroom.sort(function(a,b){
      //   return a.id - b.id;
      // })



      // 주의
      // 등호로 array를 집어넣으면 왼쪽 오른쪽값공유해주세요~임
      // this.oneroom = this.oneroomOriginal;
      this.oneroom = [...this.oneroomOriginal];
    },
    priceSortHigh(){
      this.oneroom.sort(function(a,b){
        return  b.price - a.price;
      })
    }
  },

  // 서버에서 데이터가져올 떄도 lifecycle hook 안에 코드 짬
  created(){

  },
  mounted() {
    // setTimeout(()=>{
    //   this.showDiscount = false;
    // },2000)

    var timeRate =  setInterval(()=>{
      this.할 -= 1;
      if(this.할 == 0){
        clearInterval(timeRate);
        // this.showDiscount = false;
      }
    },1000)
  },
  components: {
    Discount : Discount, 
    Modal : Modal,
    Item : Item
  }
}
</script>

<style>
/* 등장애니메이션 */
/* 시작 */
.fade-enter-from{
  opacity: 0;
} 

.fade-enter-active{
  transition: all 0.3s;
}
 /* 끝 */
.fade-enter-to{
  opacity: 1;
}


/* 퇴장애니매이션 */
/* 시작 */
.fade-leave-from{
  opacity: 1;
} 

.fade-leave-active{
  transition: all 0.3s;
}
 /* 끝 */
.fade-leave-to{
  opacity: 0;
}



.start{
  opacity: 0;
  transition: all 0.3s;
}
.end{
  opacity: 1;
}

body{
  margin:0;
}
div{
  box-sizing: border-box;
}
.black-bg{
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,.5);
  position:fixed;
  padding: 20px;;
}
.white-bg{
  width: 100%;
  background: #fff;
  border-radius: 8px;
  padding: 20px;
}
.white-bg img{
  width:100%; 
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.menu{
  background: darkslateblue;
  padding:15px;
  border-radius: 5px;
}
.menu a{
  color:#fff;
  padding:10px;
}
.room-img{
  width:100%;
  margin-top:40px;
}
.warp{
  padding:10px;
}
.card_box{margin-bottom:20px; cursor: pointer;}

.modal_close{
  background:#1AAB8A;
  color:#fff;
  border:none;
  position:relative;
  height:40px;
  font-size:1em;
  padding:0 2em;
  cursor:pointer;
  transition:800ms ease all;
  outline:none;
}
.modal_close:hover{
  background:#fff;
  color:#1AAB8A;
}
.modal_close:before,.modal_close:after{
  content:'';
  position:absolute;
  top:0;
  right:0;
  height:2px;
  width:0;
  background: #1AAB8A;
  transition:400ms ease all;
}
.modal_close:after{
  right:inherit;
  top:inherit;
  left:0;
  bottom:0;
}
.modal_close:hover:before,.modal_close:hover:after{
  width:100%;
  transition:800ms ease all;
}

</style>
