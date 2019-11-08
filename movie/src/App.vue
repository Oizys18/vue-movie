<template>
  <div id="app">
    <div class="container">
      <!-- 1-3. 호출하시오. 
        필요한 경우 props를 데이터를 보내줍니다.
      -->
      <MovieList :movies='movies' :genres='genres'/>
    </div>
  </div>
</template>

<script>
const axios = require('axios');
// 1-1. 저장되어 있는 MovieList 컴포넌트를 불러오고,
import MovieList from "./components/movies/MovieList"
export default {
  name: 'app',
  // 1-2. 아래에 등록 후
  components: {
    MovieList,
  },
  data() {
    return {
      // 활용할 데이터를 정의하시오.
      movies: [],
      genres: [],
    }
  },

  mounted() {
    console.log('Hi, The app is running')
    const MOVIESURL = "https://gist.githubusercontent.com/edu-john/9b7645f841e402ce7fab2b8b606b7c7e/raw/271285772e7dfbb9b476eb27e1b85ead683d763c/movies.json"
    const GENRESURL = "https://gist.githubusercontent.com/djohnkang/7cc43f82b5165779819e3b6ad299965b/raw/b0b5850b55806672cde4666e544b6840548159a2/genres.json"
    // 0. mounted 되었을 때, 
    // 1) 제시된 URL로 요청을 통해 data의 movies 배열에 해당 하는 데이터를 넣으시오. 
    // 2) 제시된 URL로 요청을 통해 data의 genres 배열에 해당 하는 데이터를 넣으시오.
    // axios는 위에 호출되어 있으며, node 설치도 완료되어 있습니다.
    axios.get(MOVIESURL)
      .then(result => {
        this.movies = result.data
        // .movies=(result.data)
      })
    axios.get(GENRESURL)
      .then(result => {
        this.genres = result.data
      })
  },

}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
