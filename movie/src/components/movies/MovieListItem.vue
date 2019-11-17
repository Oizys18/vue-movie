<template>
  <div class="col-3 my-3">
    <!-- img 태그에 src와 alt값(영화제목)을 설정하시오 -->
    <img class="movie--poster my-3" :src="movie.poster_url" alt="movie.poster_url" />
    <!-- 영화 제목을 출력하시오. -->
    <h5>{{ movie.name }}</h5>
    <!-- 모달을 활용하기 위해서는 data-taget에 모달에서 정의된 id값을 넣어야 합니다. -->
    <button class="btn btn-primary" data-toggle="modal" :data-target="movieid" >영화 정보 상세보기</button>
    <!-- 1-3. 호출하시오.필요한 경우 props를 데이터를 보내줍니다.-->
    <MovieListItemModal :movie='movie' /> 
  </div>
</template>

<script>

// 1-1. 저장되어 있는 MovieListItemModal 컴포넌트를 불러오고,
import MovieListItemModal from "./MovieListItemModal";
export default {
  name: "MovieListItem",
  // 1-2. 아래에 등록 후
  components: {
    MovieListItemModal
  },
  // 0. props 데이터를 받기 위하여 설정하시오.
  // movie 타입은 Object이며, 필수입니다.
  // 설정이 완료 되었다면, 상위 컴포넌트에서 값을 넘겨 주세요.
  // 그리고 적절한 곳에 사용하세요.
  props: {
    movie: {
      type: Object,
      required: true
    }
  },
  data() {
    // 활용할 데이터를 정의하시오.
    return{
      movieid: `#movie-${this.movie.id}`,
    }
  },
};
</script>

<style>
.movie--poster {
  width: 200px;
}
</style>