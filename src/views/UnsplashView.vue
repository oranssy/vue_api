<template>
  <div>
    <HeaderCont />
    <TitleCont name1="unsplash" name2="reference api" />
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
