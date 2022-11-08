<template>
  <section class="cont__contact">
    <p>Let's create something new</p>
    <h3>LET'S Get IN <em>TOUBH</em></h3>
    <a href="mailto:oranssy.daum.net">oranssy.daum.net</a>
  </section>
</template>

<style lang="scss">
// cont__contact
.cont__contact {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  color: var(--white);
  text-transform: uppercase;

  p {
    font-size: 20px;
    margin-bottom: 20px;
    font-family: var(--font-sub2);
    text-align: center;
    line-height: 1;
  }

  h3 {
    font-size: 9vw;
    font-family: var(--font-main);
    line-height: 1;
    text-align: center;

    em {
      display: block;
    }
  }

  a {
    font-size: 16px;
    font-family: var(--font-sub2);
    border: 1px solid var(--white);
    border-radius: 50px;
    padding: 1vw 4vw;
    color: var(--white);

    &:hover {
      background: #fff;
      color: #000;
    }
  }
}
</style>
