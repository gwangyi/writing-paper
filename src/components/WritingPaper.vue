<template>
  <div class="page container">
    <div v-for="(row, i) in page" :key="i" class="row">
      <svg v-for="(cell, i) in row" :key="i" class="cell" viewBox="0 0 10 10">
        <text x="50%" y="50%">{{ cell }}</text>
      </svg>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component({})
export default class WriteBook extends Vue {
  @Prop(String)
  readonly text!: string;

  get page() {
    const page = [];
    let i = 0;
    while (i < this.text.length) {
      const row = [];
      while (this.text[i] === " " && i < this.text.length) ++i;
      if (i >= this.text.length) break;

      let j = 0,
        k = 0;
      while (k < this.glyphPerRow && i + k < this.text.length) {
        if (this.text[i + j] == "\n") {
          j += 1;
          break;
        } else if (
          this.text.charCodeAt(i + j) < 256 &&
          this.text.charCodeAt(i + j + 1) < 256
        ) {
          row.push(this.text[i + j] + this.text[i + j + 1]);
          j += 2;
        } else {
          row.push(this.text[i + j]);
          j += 1;
        }
        ++k;
      }
      if (row.length > 0) {
        while (k < this.glyphPerRow) {
          row.push("");
          ++k;
        }
        page.push(row);
      }
      i += j;
    }
    return page;
  }
  get glyphPerRow() {
    return Math.max(
      Math.ceil(Math.sqrt(this.text.length / 0.7) + 1) +
        Math.ceil((this.text.match(/\n/g) || []).length * 0.35),
      10
    );
  }
}
</script>

<style scoped>
@import (
  "https://fonts.googleapis.com/css2?family=Nanum+Gothic:wght@700&display=swap"
);
.page {
  display: flex;
  flex-direction: column;
  margin: 0 0 5vh;
}
.row {
  display: flex;
  flex-direction: row;
}
.cell {
  flex: 1;
  height: auto;
  border: 1px solid black;
  margin: -0.5px;
}
.cell:before {
  content: "";
  float: left;
  padding-top: 100%;
}
svg.cell text {
  font-family: "Nanum Gothic";
  font-weight: 700;
  font-size: 9px;
  text-anchor: middle;
  dominant-baseline: central;
}
.grey text {
  fill: #ccc;
}
.transparent text {
  fill: transparent;
}
</style>
