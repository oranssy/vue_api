<template>
  <div>
    <HeaderCont />
    <TitleCont name1="reference" name2="reference api" />
    <section class="cont__refer">
      <div class="container">
        <div class="refer__inner">
          <h2>CSS</h2>
          <ul class="refer__list">
            <li v-for="refer in refers" :key="refer.title">
              <a href="#">
                <span class="num">{{ refer.num }}</span>
                <span class="name">{{ refer.title }}</span>
                <span class="desc">{{ refer.desc }}</span>
                <span class="use">{{ refer.use }}</span>
              </a>
            </li>
          </ul>
        </div>
      </div>
    </section>
    <ContactCont />
    <FooterCont />
  </div>
</template>

<script>
import HeaderCont from "@/components/HeaderCont.vue";
import TitleCont from "@/components/TitleCont.vue";
import ContactCont from "@/components/ContactCont.vue";
import FooterCont from "@/components/FooterCont.vue";
import { ref } from "vue";
export default {
  components: {
    HeaderCont,
    TitleCont,
    ContactCont,
    FooterCont,
  },
  setup() {
    const refers = ref([]);
    const references = () => {
      fetch(
        "https://raw.githubusercontent.com/oranssy/react_api/main/src/utils/reference.json"
      )
        .then((response) => response.json())
        // .then((result) => console.log(result.cssRefer))
        .then((result) => (refers.value = result.cssRefer))
        .catch((error) => console.log("error", error));
    };
    references();
    return {
      refers,
      references,
    };
  },
};
</script>

<style lang="scss">
.refer__inner {
  padding-bottom: 200px; // 확인용 임시값

  h2 {
    font-size: 30px;
    color: var(--black);
  }
}

.refer__list {
  border: 1px solid var(--bg-dark-border);

  li {
    border-bottom: 1px solid var(--bg-dark-border);

    a {
      display: flex;
      width: 100%;
      color: var(--black);
      align-items: center;
      font-family: var(--font-kor1);
      // padding: 10px;

      &:hover {
        background-color: #b18bf3b0;
        color: #000;
      }

      span {
        display: inline-block;
        padding: 15px 20px;
      }

      .num {
        flex: 1 1 5%;
        text-align: center;
        border-right: 1px solid var(--bg-dark-border);
      }

      .title {
        flex: 1 1 26%;
        text-align: center;
      }

      .desc {
        flex: 1 1 65%;
        border-right: 1px solid var(--bg-dark-border);
        font-family: var(--font-kor3);
      }
      .use {
        flex: 1 1 10%;
        text-align: center;
      }
    }
  }
}
</style>
