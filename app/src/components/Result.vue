<template>
  <div>
    <ul class="list">
      <li class="item" v-for="item of items" :key="item.trackId">   <!--反復処理を行う、親コンポーネントから送られてきたitemsの中身を繰り返している また、key属性に一意な値を設定することが推奨されてる（:を使って動的に値を設定します-->
        <div class="item-inner">
          <div class="photo">
            <img class="photo-img" :src="item.artworkUrl100" :alt=item.trackName>
          </div>
          <div class="content">
            <p><a class="track" :href="item.trackViewUrl" target="_blank">{{ item.trackName }}</a></p>
            <p><a class="artist" :href="item.artistViewUrl" target="_blank">{{ item.artistName }}</a></p>
            <div class="data"> {{ getYear(item.releaseDate) }} / {{ item.primaryGenreName }} / ￥{{ item.trackPrice }}</div>
          </div>
        </div>
      </li>
    </ul>
    <Loading class="loading" v-show="loadProgress"/> <!--値の真偽に応じて表示・非表示を切り替えるもの、ここでloadProgressの値に応じてLoadingコンポーネントの表示・非表示を切り替えている-->
  </div> 
</template>

<script>
import Loading from "@/components/Loading";
 
 
export default { 
  props: ["items", "loadProgress"],   //親コンポーネントからpropsでitemsとloadProgressを受け取る。
  components: {
    Loading,
  },
  methods: {
    getYear(dateStr) {
      const date = new Date(dateStr)
      return date.getFullYear()
    },
  },
};
</script>

<style scoped>
/* .item {
  padding: 20px 0;
}
.item:nth-of-type(even) {
  background-color: #f5f5f5;
}
.item-inner {
  display: flex;
  width: 90%;
  max-width: 600px;
  margin: auto;
}
.photo {
  flex: 0 0 150px;
}
.photo-img {
  width: 100%;
  display: block;
}
.content {
  flex: 1 1;
  padding-left: 20px;
}
.track {
  color: #42b883;
  font-size: 2rem;
  font-weight: 700;
  text-decoration: none;
}
.artist {
  display: block;
  color: #42b883;
  font-size: 1.4rem;
  font-weight: 700;
  text-decoration: none;
}
.data {
  margin-top: 1.5em;
  text-align: right;
  font-size: 1.2rem;
}
.loading {
  position: fixed;
  top: 70px;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 1;
  background: #35495e;
} */
</style>