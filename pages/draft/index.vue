<template>
  <div>
    <span>これは下書きのプレビューです。運用時はスタイルなど指定して本番に近い状態の見た目で動作確認ができます。</span>
    <div id="title"></div>
    <div id="body"></div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Draft',
  data() {
    return {
      data: {}
    }
  }, async created() {
    // https://blog.microcms.io/nuxt-jamstack-preview/
    const query = this.$route.query
    if (query.id === undefined || query.draftKey === undefined) {
      return
    }
    const { data } = await axios.get(
      `https://cms-practice.microcms.io/api/v1/news/${query.id}?draftKey=${query.draftKey}`,
      {
        // TODO 環境変数にしたほうがよいけど一旦いい。
        headers: { 'X-MICROCMS-API-KEY': 'a85dd8764e99460e92d2bdf73906732c1a56' }
      }
    )
    this.data = data
    console.log(data)
    document.getElementById('title').innerHTML = data.title
    document.getElementById('body').innerHTML = data.content

  }
}
</script>
<style>
/* 検証目的でお借りしています */
/* https://foollovers.com/te/index-nf00.html */
html, body, div, span, iframe, h1, h2, h3, h4, p, pre, del, em, img, b, i, dl, dt, dd, ol, ul, li, form, table, tbody, tr, th, td, article, aside, footer, header, nav, section {
  margin: 0;
  padding: 0;
  border: 0;
  outline: 0;
  font-size: 100%;
  vertical-align: baseline;
  background: transparent;
  box-sizing: border-box
}

article, aside, footer, header, nav, section {
  display: block
}

body {
  line-height: 1;
  overflow-wrap: break-word;
  word-wrap: break-word
}

input, textarea, select {
  font-family: inherit;
  font-size: inherit;
  color: inherit;
  vertical-align: middle;
  box-sizing: border-box
}

a {
  margin: 0;
  padding: 0;
  text-decoration: none;
  outline: none;
  font-size: 100%;
  vertical-align: baseline;
  background: transparent
}

a img {
  border-style: none
}

ul, li {
  list-style-type: none
}

.cf:before, .cf:after {
  content: " ";
  display: table
}

.cf:after {
  clear: both
}


/* ===================================
背景,文字,リンク設定
=================================== */

html {
  font-size: 62.5%
}

body {
  background: #fff; /* 背景 */
  color: #000; /* 文字色 */
  font-family: 'Segoe UI', '游ゴシック Medium', 'Yu Gothic Medium', '游ゴシック体', YuGothic, 'Hiragino Kaku Gothic ProN', 'メイリオ', Meiryo, sans-serif;
  font-size: 1.3em; /* 文字の大きさ */
  letter-spacing: .1em;
  line-height: 1.5;
  text-align: center
}

/*  リンク
------------------------------ */
a {
  color: inherit
}

a:hover {
  color: #e13b8b
}

#main-wrap a {
  color: #e13b8b;
  text-decoration: underline
}

#main-wrap a:hover {
  color: #ccc
}

/* ===================================
基本
=================================== */

#wrapper {
  margin: 20px auto;
  text-align: left;
  max-width: 800px /* 幅 */
}

header {
  padding: 0 0 20px
}

footer {
  padding: 20px 0 0;
  text-align: center
}

/* ===================================
メニュー
=================================== */

#menu {
  margin: 0 auto;
  text-align: center
}

nav li {
  display: inline-block;
  margin: 10px
}

nav li a {
  border: 2px solid #000;
  display: table-cell;
  vertical-align: middle;
  text-align: center;
  padding: 5px;
  position: relative; /* 必須 */
  height: 80px;
  width: 80px;
  max-width: 80px;
  box-sizing: border-box
}

nav li:nth-child(odd) {
  background: #000;
  color: #fff
}

nav li:nth-child(even) {
  background: #fff;
  color: #000
}

nav li a:hover {
  background: #e13b8b;
  color: #fff
}

/* ===================================
著作権表示、ページ上部へのリンク
=================================== */

#pagetop {
  background: rgba(0, 0, 0, .6);
  border-radius: 5px;
  height: 50px;
  width: 50px;
  position: fixed;
  bottom: 20px;
  right: 20px
}

.arrow {
  border-left: 3px solid #fff;
  border-top: 3px solid #fff;
  position: absolute;
  top: 40%;
  left: 36%;
  height: 14px;
  width: 14px;
  -ms-transform: rotate(45deg);
  -webkit-transform: rotate(45deg);
  transform: rotate(45deg)
}

#fl a {
  color: #fff;
  background: #000;
  border-radius: 5px;
  display: inline-block;
  margin: 20px 0;
  padding: 5px
}

/* ===================================
見出し、枠、線
=================================== */

h1 {
  font-size: 1.3em;
  letter-spacing: .1em;
  margin: 0 0 .5em 0;
  text-shadow: 5px 5px 1px #ccc
}

h2 {
  background: #000;
  color: #fff;
  font-size: 1.2em;
  margin: 1em 0 2em 0;
  padding: 10px;
  position: relative
}

h2::after {
  border: 8px solid transparent;
  border-top: 8px solid #000;
  content: '';
  position: absolute;
  top: 100%;
  left: 30px;
  height: 0;
  width: 0
}

h3 {
  border-bottom: 2px solid;
  font-size: 1.2em;
  letter-spacing: .1em;
  margin: 20px 0
}

dt {
  font-weight: 700;
  padding: 0 0 1em 0
}

dd {
  border-bottom: 1px solid;
  margin: 0 0 1em 1em
}

em {
  font-style: normal;
  font-weight: 700
}

input, textarea {
  background: #fff;
  border: 2px solid;
  margin: 3px 0;
  width: 100%
}

textarea {
  height: 50px
}

hr {
  display: block;
  border: 0;
  border-top: 1px solid #ccc;
  margin: 1em 0;
  padding: 0;
  height: 1px
}

.marker {
  background: #ea75ac;
  background: -webkit-linear-gradient(rgba(234, 117, 172, 0) 50%, #ea75ac 0%);
  background: linear-gradient(rgba(234, 117, 172, 0) 50%, #ea75ac 0%)
}

.dcline {
  border-left: 8px solid #000;
  margin: 5px 0;
  padding: 3px
}

.textbox {
  border: 2px solid;
  margin: 10px 0;
  padding: 3px;
  text-align: center
}

.title {
  color: #e13b8b;
  font-size: 1.5em;
  font-weight: 700;
  letter-spacing: .1em;
  margin: 2em 0;
  text-align: right
}

.txt {
  border-left: 1px solid #999;
  margin: 1em;
  padding: 0 0 0 1em
}

.frame {
  background: #e13b8b;
  border-radius: 3px;
  padding: 7px
}

/*  文字の下の線
------------------------------ */
/* bodyのfont-sizeを変更したら数値を変更 */
/* 2.6 = font-size:1.3 x line-height:2 */
.line {
  padding-bottom: 0.1em;
  background-color: #fff;
  background-image: -webkit-linear-gradient(left, #fff 1.1px, rgba(255, 255, 255, 0) 1px), -webkit-linear-gradient(top, #666 1.1px, rgba(102, 102, 102, 0) 1px);
  background-image: linear-gradient(to right, #fff 1.1px, rgba(255, 255, 255, 0) 1px), linear-gradient(to bottom, #666 1.1px, rgba(102, 102, 102, 0) 1px);
  background-size: 2px 2.6rem;
  line-height: 2
}

/* ===================================
横幅800pxで切り替え
=================================== */

@media screen and (max-width: 800px) {
  #wrapper {
    margin: 20px 20px 50px
  }
}

/* ===================================
スマホ、タブレット用
横幅600pxで切り替え
=================================== */

@media screen and (max-width: 600px) {
  body {
    font-size: 1.5em
  }

  #contents {
    padding: 20px 0
  }

  #contents a:not(.bg-none) {
    color: #fff;
    background: #e13b8b;
    border-radius: 5px;
    display: inline-block;
    margin: 3px 3px 3px 0;
    padding: 3px;
    text-decoration: none
  }

  nav li {
    margin: 5px
  }

  /*  文字の下の線
  ------------------------------ */
  /* bodyのfont-sizeを変更したら数値を変更 */
  /* 3 = font-size:1.5 x line-height:2 */
  .line {
    background-size: 2px 3rem;
    line-height: 2
  }

  /* 画像の縮小表示
  ------------------------------ */
  img {
    max-width: 100%;
    height: auto
  }
}

</style>
