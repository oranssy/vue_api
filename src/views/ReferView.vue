<template>
  <div>
    <HeaderCont />
    <TitleCont name1="CSS Reference" name2="Using API" />
    <section class="cont__refer">
      <div class="container">
        <div class="refer__inner">
          <h2>CSS Property</h2>
          <ul class="refer__list">
            <li v-for="refer in refers" :key="refer.title">
              <span>
                <em class="num">{{ refer.num }}</em>
                <em class="title">{{ refer.title }}</em>
                <em class="desc">{{ refer.desc }}</em>
                <em class="use">{{ refer.use }}</em>
              </span>
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
    margin-bottom: 20px;
  }
}

.refer__list {
  li {
    border-top: 1px solid var(--bg-dark-border);
    border-bottom: 1px solid var(--bg-dark-border);
    color: var(--black);

    span {
      display: flex;
      width: 100%;
      color: #727272;
      align-items: center;
      font-family: var(--font-kor3);
      font-size: 18px;
      padding: 5px 15px;

      &:hover {
        background-color: #c0ade04b;
        color: var(--black);
      }

      em {
        display: inline-block;
        padding: 15px 8px;
      }
      em:nth-child(1) {
        // flex: 1 1 5%;
        text-align: center;
        padding: 15px 20px;
        border-right: 1px solid #2f2f2f;
      }
      em:nth-child(2) {
        // flex: 1 1 30%;
        width: 16%;
        text-align: center;
        font-family: var(--font-kor2);
        border-right: 1px solid #2f2f2f;
      }
      em:nth-child(3) {
        // flex: 1 1 65%;
        width: 70%;
        border-right: 1px solid #2f2f2f;
      }
      em:nth-child(4) {
        // flex: 1 1 65%;
        width: 10%;
      }
      .use {
        // flex: 1 1 10%;
        width: 7%;
        text-align: center;
      }
    }
  }
}

// span {
//   display: inline-block;
//   padding: 15px 20px;
// }

// .num {
//   flex: 1 1 5%;
//   text-align: center;
//   border-right: 1px solid var(--bg-dark-border);
// }

// .title {
//   flex: 1 1 26%;
//   text-align: center;
//   font-family: var(--font-main);
// }

// .desc {
//   flex: 1 1 65%;
//   border-right: 1px solid var(--bg-dark-border);
//   font-family: var(--font-kor3);
// }
// .use {
//   flex: 1 1 10%;
//   text-align: center;
// }
</style>
