# Project_09

## 1. 목표

- Node 개발 환경과 webpack에 대한 이해 
- 컴포넌트 기반의 구조에 대한 이해 
- axios를 통한 비동기적 데이터 처리에 대한 이해 
- Vue.js 개발 프로세스를 통한 영화 목록 페이지 구현 

## 2. 구현

### axios로 데이터 받기

- 모든 vue에서 사용될 데이터기 때문에 최상단인 `App.vue`에서 받는다.
- `mounted()`를 사용해서 vue의 `Creation` 이후 로드한다.

```javascript
mounted() {
    const MOVIESURL = "https://gist.githubusercontent.com/edu-john/9b7645f841e402ce7fab2b8b606b7c7e/raw/271285772e7dfbb9b476eb27e1b85ead683d763c/movies.json"
    const GENRESURL = "https://gist.githubusercontent.com/djohnkang/7cc43f82b5165779819e3b6ad299965b/raw/b0b5850b55806672cde4666e544b6840548159a2/genres.json"
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
```

- data에 저장

```javascript
data() {
    return {
      movies: [],
      genres: [],
    }
```

### 부모-자식 간 데이터 송수신

- `vue`의 `props` 사용: 부모->자식만 사용했기 때문에 `events`는 불필요
  - Vue.js에서 부모-자식 컴포넌트 관계는 **props는 아래로, events 위로** 라고 요약 할 수 있습니다. 부모는 **props**를 통해 자식에게 데이터를 전달하고 자식은 **events**를 통해 부모에게 메시지를 보냅니다. 

- `App.vue`

  ```javascript
  data() {
      return {
        movies: [],
        genres: [],
      }
    },
  ```

  - `MovieList`: 영화 목록 표시, 장르 선택 기능 

    ```html
    <MovieListItem :movie="movie" v-for="movie in selectedMovies" :key="movie.id" />
    ```

    ```javascript
    props: {
        movies: {
          type: Array,
          required: true
        },
        genres: {
          type: Array,
          required: true
        }
      },
    ```

  - `MovieListItem`: 개별 영화

    ```html
    <MovieListItemModal :movie='movie' /> 
    ```

    ```javascript
    props: {
        movie: {
          type: Object,
          required: true
        }
      },
    ```

  - `MovieListItemModal`: 개별 영화 Modal 상세보기

    ```javascript
    props:{
        movie: {
          type:Object,
          required:true,
        },
    ```



### 상세보기 Modal 구현

#### 1. `MovieListItem.vue`

- `data-target`에 모달에서 정의한 id 값을 넣는다.

```html
<button class="btn btn-primary" data-toggle="modal" :data-target="movieid" >영화 정보 상세보기</button>
```

- Modal vue 호출

```html
<MovieListItemModal :movie='movie' /> 
```

#### 2.`MovieListItemModal.vue`

- 영화별 고유 모달을 위해 id 속성을 정의
  - `integer`로는 못한다. `string`으로 해야함

```html
<div class="modal fade" tabindex="-1" role="dialog" :id="movieid">
```

- 부모로부터 `movie`데이터를 `props`를 통해 받는다.

```javascript
props:{
    movie: {
      type:Object,
      required:true,
    },
```

- data에서 `movieid`정의

```javascript
data() {
    return {
      // 백틱으로 만들어준다.
      movieid:`movie-${this.movie.id}`, 
    }
```

## 3. Retrospect

```
props를 통해 부모로부터 데이터를 받아 사용하는 연습이 되었다. 
axios의 사용이나 props 설정, 데이터 사용은 무난하게 구현했다.
하지만 Modal을 구현할 때 id속성을 정의하고 data-toggle을 하는 것이 매우 복잡하고 어려웠다.
bootstrap에 대한 공부도 부족한 것 같다...
```



