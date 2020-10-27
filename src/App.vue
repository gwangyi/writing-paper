<template>
  <div id="app">
    <section class="hero is-primary screen-only">
      <div class="hero-body">
        <div class="container">
          <h1 class="title">
            쓰기 연습장 생성기
          </h1>
          <h2 class="subtitle">
            문구를 넣으면 연습용 원고지를 만들어줍니다.
          </h2>
        </div>
      </div>
    </section>
    <section class="section">
      <div class="container screen-only">
        <b-field>
          <b-input maxlength="200" type="textarea" v-model="text"></b-input>
        </b-field>
      </div>
      <b-button
        class="screen-only"
        type="is-primary"
        icon="print"
        expanded
        @click="print"
      >
        Print
      </b-button>
      <div class="container">
        <div class="datename">날짜: {{ today }}, 이름:</div>
        <WritingPaper class="grey" :text="text" />
        <WritingPaper class="transparent" :text="text" />
      </div>
    </section>
    <footer class="footer">
      <div class="content has-text-centered">
        <p>
          쓰기연습장 생성기 &copy; Sungkwang Lee
          <a href="http://gwangyi.github.io/" class="screen-only">
            <b-icon icon="home" size="is-small" />
          </a>
        </p>
        <p class="screen-only">
          Icons made by
          <a href="https://www.flaticon.com/authors/freepik" title="Freepik"
            >Freepik</a
          >
          from
          <a href="https://www.flaticon.com/" title="Flaticon">
            www.flaticon.com</a
          >
        </p>
      </div>
    </footer>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import WritingPaper from "./components/WritingPaper.vue";

@Component({
  components: {
    WritingPaper
  }
})
export default class App extends Vue {
  private text =
    "여기에 문장을 쓰세요. 반각 문자는 두 글자가 한 칸에 들어갑니다. abcde.";

  get today() {
    return new Date().toLocaleDateString();
  }

  private print() {
    window.print();
  }
}
</script>

<style lang="scss">
// Import Bulma's core
@import "~bulma/sass/utilities/_all";

// Set your colors
$primary: #ef8c67;
$primary-invert: findColorInvert($primary);

$colors: (
  "white": (
    $white,
    $black
  ),
  "black": (
    $black,
    $white
  ),
  "light": (
    $light,
    $light-invert
  ),
  "dark": (
    $dark,
    $dark-invert
  ),
  "primary": (
    $primary,
    $primary-invert
  ),
  "info": (
    $info,
    $info-invert
  ),
  "success": (
    $success,
    $success-invert
  ),
  "warning": (
    $warning,
    $warning-invert
  ),
  "danger": (
    $danger,
    $danger-invert
  )
);

// Import Bulma and Buefy styles
@import "~bulma";
@import "~buefy/src/scss/buefy";

@media print {
  .screen-only {
    display: none !important;
  }
}
@media screen {
  .print-only {
    display: none !important;
  }
}

.datename {
  font-size: 5vw;
}
</style>
