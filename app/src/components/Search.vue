<template>
  <div>
    <div class="container"> 
      <div class="title">Video-On-Demand 横断検索</div>
      <input class="text" type="text" v-model="term" v-on:keyup.enter="exe">   <!--双方向データバインディングを行うもの、inputの値とdataの値が常に同期される-->
      <button class="submit" type="submit" value="Search" v-on:click="exe">検索</button>  <!--イベントを購読するもの、JSで例えるとaddEventListener @はv-onの省略記法-->
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
      const { data } = await axios.get(`https://itunes.apple.com/search?term=${this.term}&country=jp&entity=movie`);
      // const { data } = await axios.get(`/v1/requests?state=open&country=US,CA&title=${this.title}&packageId=12345,22222&sourceType=subs&sourceLanguage=en&requestStatus=redelivery_requested&contentPartner=1cf3dfc6-8a88-4efb-bd28-959d19fe074a&since=2016-04-01T00:00:00.000+0000&until=2016-04-15T00:00:00.000+0000&inspectionStatus=success`);
      this.$emit("loadComplete", { results: data.results })
    },
  },
};
</script>

<style scoped>
.title{
  color:#fff;
  font-size: 20px;
  margin: auto;
  margin-left: 50px;
  /* margin-right: 100px; */
}

.container {
  display: flex;
  justify-content: center;
  height: 70px;
  padding: 20px;
  background-color: rgb(30, 30, 30);
  /* background-color: black; */
  box-sizing: border-box;
}
 
 
.text {
  outline: none;
  width: 50%;
  max-width: 300px;
  padding: .5em;
  border: none;
}
 
 
.submit {
  outline: none;
  padding: .5em 2em;
  margin-left: 10px;
  border: none;
  border-radius: 20px;
}

.submit {
  display: inline-block;
  padding: 0.5em 1em;
  text-decoration: none;
  border-radius: 4px;
  color: #ffffff;
  background-image: linear-gradient(#6795fd 0%, #67ceff 100%);
  box-shadow: 0px 2px 2px rgba(0, 0, 0, 0.29);
  border-bottom: solid 3px #5e7fca;
}

.submit:active {
  -webkit-transform: translateY(4px);
  transform: translateY(4px);
  box-shadow: 0px 0px 1px rgba(0, 0, 0, 0.2);
  border-bottom: none;
}
</style>