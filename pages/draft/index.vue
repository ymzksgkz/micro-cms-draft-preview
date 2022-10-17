<template>
  <div>
    <span style="font-size: 12px;">これは下書きのプレビューです。運用時はスタイルなど指定して本番に近い状態の見た目で動作確認ができます。</span>
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
<style lang="css">

body {
  background-color: #f9fafc;
}

#title {
  margin: 30px 40px;
  font-family: "ヒラギノ角ゴ Pro W3", "Hiragino Kaku Gothic Pro", "メイリオ", Meiryo, "ＭＳ Ｐゴシック", sans-serif;
  color: #001350;
  font-size: 28px;
}

#body {
  background-color: #d0d8dd10;
  box-shadow: 0 -3px 20px rgb(44 93 255 / 10%);
  margin: 40px 32px;
  padding: 32px 40px;
  font-family: "ヒラギノ角ゴ Pro W3", "Hiragino Kaku Gothic Pro", "メイリオ", Meiryo, "ＭＳ Ｐゴシック", sans-serif;
  font-size: 14px;
  color: #001350;
  line-height: 20px;
  letter-spacing: 0.67px;
}

h1, h2, h3, h4, h5 {
  letter-spacing: 1.5px;
  line-height: 1.2;
}

h1 {
  font-size: 50px;
}

h2 {
  font-size: 40px;
}

h3 {
  font-size: 30px;
}

h4 {
  font-size: 20px;
}

h5 {
  font-size: 10px;
}

blockquote {
  background-color: #50135020;
  padding: 12px 20px;
  margin: 0;
  max-width: 60%;
}

code {
  padding: 5px 5px;
  border-radius: 3px 3px;
  background-color: #d0135010;
  color: #ff6666;
  letter-spacing: 1px;
}

pre {
  white-space: pre-wrap;
  display: block;
  max-width: 60%;
}

pre > code {
  padding: 12px 20px;
  width: 100%;
  background-color: black;
  color: white;
  display: block;
}

</style>
