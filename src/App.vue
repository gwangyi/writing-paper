<template>
  <div id="app">
    <section class="hero is-primary screen-only">
      <div class="hero-body">
        <div class="container">
          <h1 class="title">
            <img class="logo" src="./assets/logo.png" />
            쓰기 연습장 생성기
          </h1>
          <h2 class="subtitle">
            문구를 넣으면 연습용 원고지를 만들어줍니다.
          </h2>
        </div>
      </div>
    </section>
    <section class="section body">
      <div class="container screen-only">
        <b-field>
          <b-input maxlength="200" type="textarea" v-model="text"></b-input>
        </b-field>
        <b-button
          class="screen-only"
          type="is-primary"
          icon-left="printer"
          expanded
          @click="print"
        >
          Print
        </b-button>
      </div>
      <div class="container">
        <div class="datename print-only">날짜: {{ today }}, 이름:</div>
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
import { Component, Watch, Vue } from "vue-property-decorator";
import WritingPaper from "./components/WritingPaper.vue";

const DEFAULT_TEXT =
  "여기에 문장을 쓰세요. 반각 문자는 두 글자가 한 칸에 들어갑니다. abcde.";

@Component({
  components: {
    WritingPaper
  }
})
export default class App extends Vue {
  private text =
    decodeURIComponent(new URL(location.href).hash.substr(1)) || DEFAULT_TEXT;

  @Watch("text")
  private onText() {
    history.replaceState({}, "", "#" + this.text);
  }

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
  .footer {
    padding: 0;
    margin-top: -3rem;
  }
  .section.body {
    padding-top: 0;
  }
}
@media screen {
  .print-only {
    display: none !important;
  }
}

.datename {
  font-size: 1.5rem;
}

h1 img.logo {
  height: 1em;
}
</style>
