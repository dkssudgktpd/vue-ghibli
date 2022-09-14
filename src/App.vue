<template>
<div class="wrap">
  <div class="container">
    <Transition name="fade">
    <div class="intro" v-if="show"></div>
    </Transition>
  <RouterView @hide="hideIntro"/>
  </div>
</div>
</template>

<script>

import {useStore} from 'vuex'
import {ref} from 'vue'
export default {
setup(){
  // vuex에 dispatch 전송
  const store = useStore();
  store.dispatch('fetchMovieList')
  // 인트로 화면관련
  const show = ref(true)
  const hideIntro = () => {
    show.value = false;
    // html의 overflow-y 를 auto로 셋팅해야한다
    document.querySelector('html').style.overflowY = 'auto'
  }
  return{
    show,hideIntro
  }
}
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

ul,li{
  list-style: none;
}

a{
  text-decoration: none;
  color: #333;
}

/* scrollbar */
::-webkit-scrollbar {
  width: 8px;
  height: 5px;
  background-color: lightblue;
  -moz-border-radius: 0px;
  -webkit-border-radius: 0px;
  border-radius: 0px;
}

::-webkit-scrollbar-thumb {
  background-color: rgb(77, 187, 255);
  -moz-border-radius: 2px;
  -webkit-border-radius: 2px;
  border-radius: 2px;
}
html{
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  font-size: 16px;
  background: lightblue;
  overflow-x: hidden;
  overflow-y: hidden;
}

.wrap{
  position: relative;
  display: block;
  
}

.container{
  position: relative;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}
.intro{
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100vh;
  background: url('@/assets/intro.jpg') no-repeat center;
  background-size: cover;
  z-index: 99;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>