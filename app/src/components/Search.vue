<template>
  <div>
    <div class="container"> 
      <input class="text" type="text" v-model="term" @keyup.enter="exe">   <!--双方向データバインディングを行うもの、inputの値とdataの値が常に同期される-->
      <input class="submit" type="submit" value="Search" @click="exe">  <!--イベントを購読するもの、JSで例えるとaddEventListener @はv-onの省略記法-->
    </div>
  </div>
</template>

<script>
import axios from "axios";
 
 
export default {
  data() {
    return {
      term: "",
    }
  },
  methods: {
    async exe() {   
      this.$emit("loadStart")    //$emit イベントを送出するもので、JavaScriptで例えるとdispatchEvent   取得したデータを$emitを通じて、親コンポーネントで受け取れるようにする。
    //   const { data } = await axios.get(`//itunes.apple.com/search?term=${this.term}&country=jp&entity=musicVideo`);
      const { data } = await axios.get(`https://itunes.apple.com/search?term=${this.term}&country=jp&entity=movie`);
      this.$emit("loadComplete", { results: data.results })
    },
  },
};
</script>

<style scoped>
/* .container {
  display: flex;
  justify-content: center;
  height: 70px;
  padding: 20px;
  background-color: #35495e;
  box-sizing: border-box;
}
 
 
.text {
  width: 50%;
  max-width: 300px;
  padding: .5em;
  border: none;
}
 
 
.submit {
  padding: .5em 2em;
  margin-left: 10px;
  color: #fff;
  background-color: #42b883;
  border: none;
  border-radius: 20px;
} */
</style>