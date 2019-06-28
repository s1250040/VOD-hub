<template>
  <div class="root">
    <Search class="search" @loadStart="onLoadStart" @loadComplete="onLoadComplete"/><!-- SearchコンポーネントからloadStart/loadCompleteイベントを購読する -->
    <Result :items="items" :loadProgress="loadProgress"/><!-- ResultコンポーネントにitemsとloadProgressを送る -->
  </div>
</template>


<script>
import Search from "@/components/Search";
import Result from "@/components/Result";
export default {
  data() {
    return {
      items: [],    //dataのitemsにはAPIから取得したデータを入れる
      loadProgress: false,    //loadProgressにはローディングの状態が入る
    };
  },
  methods: {
    onLoadStart() {
      this.loadProgress = true;    //イベント時に実行するイベントハンドラ
    },
    onLoadComplete({ results }) {
      this.items = results;         //イベント時に実行するイベントハンドラ
      this.loadProgress = false;
    },
  },
  components: {
    Search,
    Result,
  },
};
</script>


<style scoped>
.root {
  padding-top: 70px;
}
 
 
.search {
  width: 100%;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 1;
}
</style>
 
 
<style>
html {
  font-size: 62.5%;
}
body {
  margin: 0;
  color: #35495e;
}
p {
  margin: 0;
}
ul {
  padding: 0;
  margin: 0;
}
</style>

