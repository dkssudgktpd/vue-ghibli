<template>

  <div class="movie" v-for="(item, index) in movieList" :key="index">
    <MovieList :item="item"/>
  </div>
  <button class="gotop" ref="gotop" @click="moveTop">Top</button>
</template>

<script>
import {useStore} from 'vuex'
import {computed,onUpdated,ref} from 'vue'
import MovieList from '../components/MovieList.vue'
export default {
components : {MovieList},
setup(props, context){
  const store = useStore();
  // 처음에는 computed의 결과가 없는 상태
  const movieList = computed(() => store.getters.getMovieList)
  // html 태그의 속성으로 ref를 활용하여 선택
  
  const gotop = ref(null)
  // ref를 참조하려면 onMounted를 사용해야함

  // axios 실행 > vuex : mutation 실행
  onUpdated(() => {
    // 내용물이 업데이트가 되었다면 App으로 intro가 사라지라고 hide 신호를 보낸다.
    let delay = setTimeout(()=>{
      clearTimeout(delay)
      context.emit('hide') 
    },1000)
  })
  const moveTop = () => {
    window.scrollTo({
      top : 0,
      left : 0,
      behavior: 'smooth'
    });
  }
  return{
    movieList,gotop,moveTop
  }
}
}
</script>

<style scoped>
.movie{
  position: relative;
  display: block;
  width: 47%;
  background: #fff;
  margin: 35px 0;
  border-radius: 5px;
  color: #adaeb9;
  padding: 20px;
  box-shadow: 0 13px 27px -5px rgba(50, 50, 93, 0.25),
            0 8px 16px -8px rgba(0, 0, 0, 0.3),
            0 -6px 16px -6px rgba(0, 0, 0, 0.025);
  cursor: pointer;
}
.movie img{
  width: 100%;
}
.gotop{
  position: fixed;
  right: 50px;
  bottom: 150px;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  text-align: center;
  line-height: 50px;
  background-color: lightskyblue;
  color: #ddd;
  cursor: pointer;
  z-index: 9;
  border: 0;
  font-size: 18px;
  font-weight: 500;
  transition: background-color 0.3s;
}
.gotop:hover{
  color: #fff;
  background-color: rgb(88, 191, 255);
}
@media screen and (max-width: 1000px) {
  .movie{
    width: 95%
  }
}
</style>