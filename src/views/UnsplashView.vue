<template>
  <div>
    <HeaderCont />
    <TitleCont name1="Unsplash list" name2="using API" />
    <section class="cont__refer">
      <div class="container">
        <div class="unsplash__inner">
          <div class="unsplash__slider"></div>
          <div class="unsplash__search"></div>
          <div class="unsplash__images">
            <ul>
              <li v-for="splash in splashes" :key="splash.id">
                <a href="#">
                  <img :src="splash.urls.regular" :alt="splash.id" />
                </a>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </section>
    <ContactCont />
    <FooterCont />
  </div>
</template>

<script>
import HeaderCont from "@/components/HeaderCont.vue";
import FooterCont from "@/components/FooterCont.vue";
import TitleCont from "@/components/TitleCont.vue";
import ContactCont from "@/components/ContactCont.vue";
import { ref } from "vue";
// import { response } from "express";

export default {
  components: {
    HeaderCont,
    FooterCont,
    TitleCont,
    ContactCont,
  },

  setup() {
    const splashes = ref([]);
    const search = ref("landscape");

    // const SearchSplashes = () => {
    //   fetch(
    //     "https://api.unsplash.com/search/photos?client_id=gjVsZ-zpevOV0p4hAa4Bll-1Ef-aJdelgd0Wfq5-XUE&query=${search.value}"
    //   )
    //     .then((response) => response.json())
    //     .then((result) => console.log(result))
    //     .catch((error) => console.log(error));
    // };
    // SearchSplashes();

    const RandomSplashes = () => {
      fetch(
        "https://api.unsplash.com/photos/random?client_id=gjVsZ-zpevOV0p4hAa4Bll-1Ef-aJdelgd0Wfq5-XUE$count=20"
      )
        .then((response) => response.json())
        // .then((result) => console.log(result))
        .then((result) => (splashes.value = result))
        .catch((error) => console.log(error));
    };
    RandomSplashes();

    return {
      splashes,
      search,
      // SearchSplashes,
      RandomSplashes,
    };
  },
};
</script>

<style lang="scss">
// 이미지 슬라이더
#unsplash__list {
  width: 100%;
  height: 650px;
  overflow: hidden;

  h2 {
    display: inline-block;
    color: var(--white);
    margin-bottom: 5px;
    padding: 0 18%;
  }

  .container {
    margin-bottom: 30px;
  }

  .unsplashList__inner {
    position: absolute;
    left: 50%;
    width: 25%;
    height: 25%;
    transform: translate(-50%, 0);

    // ul {
    //   display: flex;
    //   flex-wrap: wrap;
    //   justify-content: space-between;
    // }

    .swiper-slide {
      transition: transform 0.2s ease;
      li {
        padding: 5%;
        border: 1px solid rgba(255, 255, 255, 0.2);
        margin-bottom: 70px;

        &:hover {
          transform: scale(1.05);
        }

        a {
          img {
            border-radius: 5px;
          }
        }
      }
    }
  }
}

// 이미지 검색창
.unsplash__search {
  margin-bottom: 20px;

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
      background: #1f2126;
      border: 1px solid #101626;
      color: var(--white);
    }
  }
}

// 대표 이미지 버튼
.unsplash__btn {
  margin-bottom: 70px;

  .container {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    padding: 0 50px;

    button {
      width: 100px;
      padding: 5px 8px;
      border-radius: 50px;
      font-family: var(--font-kor2);
      font-weight: bold;
      font-size: 14px;
      color: #101626;
      cursor: pointer;

      &:hover {
        background: #101626;
        border: 1px solid #383838;
        color: var(--white);
      }
    }
  }
}

// 기본 이미지
#cont__unsplash {
  .unsplash__inner {
    ul {
      column-count: 4;
      column-gap: 20px;
      width: 100%;

      li {
        margin-bottom: 20px;

        img {
          border-radius: 5px;
        }
      }
    }
  }
}
</style>
