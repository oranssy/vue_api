<template>
  <div>
    <HeaderCont />
    <TitleCont name1="List of movies" name2="using API" />
    <section class="cont__list">
      <h2>Popular List</h2>
      <div class="container">
        <div class="list__inner">
          <div class="movie__slider">
            <swiper
              :effect="'coverflow'"
              :grabCursor="true"
              :centeredSlides="true"
              :initialSlide="5"
              :slidesPerView="'auto'"
              :autoplay="{
                delay: 2500,
                disableOnInteraction: false,
              }"
              :coverflowEffect="{
                rotate: 50,
                stretch: 0,
                depth: 100,
                modifier: 1,
                slideShadows: false,
              }"
              :pagination="true"
              :modules="modules"
              class="mySwiper"
            >
              <swiper-slide v-for="(slider, index) in sliders" :key="slider.id">
                <li>
                  <div class="popularNum">{{ index + 1 }}</div>
                  <a :href="`https://image.tmdb.org/movie/${slider.id}`">
                    <img
                      :src="`https://image.tmdb.org/t/p/w500/${slider.poster_path}`"
                      :alt="slider.title"
                    />
                    <em>
                      <span class="title">{{ slider.title }}</span>
                      <span class="star">★ {{ slider.vote_average }}</span>
                    </em>
                  </a>
                </li>
              </swiper-slide>
            </swiper>
          </div>
          <!-- movie__slider -->

          <div class="movie__search">
            <div class="container">
              <h2>검색하기</h2>
              <form @submit.prevent="SearchMovies()">
                <input
                  type="search"
                  id="search"
                  placeholder="검색할 텍스트를 입력해주세요."
                  v-model="search"
                />
                <button type="submit">검색</button>
              </form>
            </div>
          </div>
          <!-- //movie__search -->

          <div class="cont__movie">
            <div class="container">
              <div class="movie__inner">
                <ul>
                  <li v-for="movie in movies" :key="movie.id">
                    <a :href="`https://image.tmdb.org/movie/${movie.id}`">
                      <img
                        :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`"
                        :alt="movie.title"
                      />
                      <em>
                        <span class="title">{{ movie.title }}</span>
                        <span class="star">★ {{ movie.vote_average }}</span>
                      </em>
                    </a>
                  </li>
                </ul>
              </div>
            </div>
          </div>
          <!-- //cont__movie -->
        </div>
      </div>
    </section>
    <FooterCont />
    <ContactCont />
  </div>
</template>

<script>
import HeaderCont from "@/components/HeaderCont.vue";
import FooterCont from "@/components/FooterCont.vue";
import TitleCont from "@/components/TitleCont.vue";
import ContactCont from "@/components/ContactCont.vue";
import { ref } from "vue";
import { Swiper, SwiperSlide } from "swiper/vue";

// Import Swiper styles
import "swiper/css";
import "swiper/css/effect-coverflow";
import "swiper/css/pagination";
// import "./style.css";

import { EffectCoverflow, Pagination, Autoplay } from "swiper";

export default {
  components: {
    HeaderCont,
    FooterCont,
    TitleCont,
    ContactCont,
    Swiper,
    SwiperSlide,
  },

  setup() {
    const movies = ref([]);
    const sliders = ref([]);
    const search = ref("disney");

    // async, await 데이터 다운이 늦을 수 있어서 비동기적으로 넣어주는 것임. 리엑트에도 같은 형식으로 넣어줌
    const SearchMovies = async () => {
      await fetch(
        `https://api.themoviedb.org/3/search/movie?api_key=1ea57f2063af5c274ebfea0573b7df9a&query=${search.value}&page=1`
      )
        .then((response) => response.json())
        .then((result) => {
          console.log(result);
          movies.value = result.results;
          search.value = "";
        })
        .catch((error) => console.log(error));
    };
    SearchMovies();

    const TopMovies = () => {
      fetch(
        `https://api.themoviedb.org/3/movie/popular?api_key=1ea57f2063af5c274ebfea0573b7df9a&language=en-US&page=1`
      )
        .then((response) => response.json())
        .then((result) => (sliders.value = result.results))
        .catch((error) => console.log(error));
    };
    TopMovies();

    return {
      movies,
      sliders,
      search,
      SearchMovies,
      modules: [EffectCoverflow, Pagination, Autoplay],
    };
  },
};
</script>

<style lang="scss">
// 인기 순위 목록 (슬라이더)
.cont__list {
  width: 100%;
  height: 740px;
  overflow: hidden;

  h2 {
    color: var(--black);
    margin-bottom: 40px;
    padding: 0 18%;
    font-weight: bold;
  }

  .container {
    margin-bottom: 30px;
  }

  .list__inner {
    // width: 100%;
    padding: 5%;

    // ul {
    //   display: flex;
    //   flex-wrap: wrap;
    //   justify-content: space-between;
    // }

    .swiper-slide {
      // width: 100%;
      width: 32%;

      li {
        // justify-content: space-between;
        // width: 30%;
        text-align: center;
        padding: 16px;
        border: 2px solid rgba(144, 144, 144, 0.29);
        position: relative;
        // margin-right: 15px;
        transition: transform 0.2s ease;
        margin-bottom: 70px;

        &:hover {
          transform: scale(1.1);
        }

        &:hover .title {
          color: var(--black);
        }

        &:hover .star {
          background: #031035;
          color: var(--white);
        }

        .popularNum {
          font-size: 50px;
          font-weight: 100;
          -webkit-text-stroke: 1px var(--white);
          -webkit-text-fill-color: transparent;
          position: absolute;
          left: 10%;
          top: 2%;
        }

        a {
          em {
            color: var(--black);

            .title {
              display: inline-block;
              padding: 10px 0;
              font-family: var(--font-kor3);
              color: rgba(0, 0, 0, 0.4);
            }

            .star {
              background: rgba(255, 255, 255, 0.5);
              color: #040814;
              position: absolute;
              right: 16px;
              top: 16px;
              width: 46px;
              height: 26px;
              border-radius: 10px;
              box-shadow: rgba(0, 0, 0, 0.5) 2px 2px 2px;
              text-align: center;
              font-family: var(--font-kor3);
              font-size: 14px;
              line-height: 28px;
              font-weight: bold;
            }
          }
        }
      }
    }
  }
}

// 검색창
.movie__search {
  margin-bottom: 100px;

  .container {
    position: relative;
  }

  h2 {
    color: var(--white);
    font-size: 40px;
    text-indent: -9999px;
    height: 0;
  }

  input {
    background: #000;
    border: 2px solid var(--white);
    border-radius: 50px;
    color: var(--white);
    width: 100%;
    padding: 10px 30px;
    font-family: var(--font-kor3);
  }

  button {
    position: absolute;
    right: 6px;
    top: 6px;
    width: 70px;
    height: 35px;
    border-radius: 50px;
    border: 0;
    font-family: var(--font-kor3);
    cursor: pointer;
    z-index: 1000;

    &:hover {
      background: #101626;
      color: var(--white);
    }
  }
}

// 기본 정보
.movie__inner {
  ul {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;

    li {
      width: 23%;
      position: relative;
      border: 2px solid rgba(196, 196, 188, 0.296);
      background: rgba(233, 231, 224, 0.516);
      padding: 20px;
      margin-bottom: 36px;
      transition: transform 0.2s ease;

      &:hover {
        transform: scale(1.125);
      }

      &:hover .title {
        color: var(--black);
      }

      &:hover .star {
        background: rgba(0, 0, 0, 0.7);
        color: var(--white);
      }

      em {
        display: block;
        height: 60px;
        // margin-bottom: 30px;
        font-family: var(--font-kor3);
        text-align: right;
      }

      .title {
        padding: 10px 0;
        display: inline-block;
        color: rgba(0, 0, 0, 0.4);
      }

      .star {
        background: rgba(88, 88, 88, 0.318);
        color: rgba(255, 255, 255, 0.5);
        position: absolute;
        left: 20px;
        top: 20px;
        width: 50px;
        height: 30px;
        border-radius: 10px;
        box-shadow: rgba(0, 0, 0, 0.5) 2px 2px 2px;
        text-align: center;
        font-size: 14px;
        line-height: 32px;
        font-weight: bold;
      }
    }
  }

  a {
    color: var(--black);
  }
}
</style>
