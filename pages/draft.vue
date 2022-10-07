<template>
  <div>
    <span>ドラフトページですaaa</span>
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

  }
}
</script>
